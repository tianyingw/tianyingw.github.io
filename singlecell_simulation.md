---
layout: page
title: Simulation Details
---

This document provides an implementation of the simulation. We followed the method in Chang Su’s paper and assessed two estimators: R.cscore is estimated via the iteratively reweighted least squares approach, and the other is our proposed rank-based estimator R.rank.
(Created by Mujin Zhou)

## 1.download raw data and packages and preprocess
```R
## Load devtools for installing R packages from Github
library(devtools)
## Install CS-CORE from Github
install_github("ChangSuBiostats/CS-CORE")
library(CSCORE)
library(Seurat)
```
```R
## download data
url = "https://hosted-matrices-prod.s3-us-west-2.amazonaws.com/Single_cell_atlas_of_peripheral_immune_response_to_SARS_CoV_2_infection-25/blish_covid.seu.rds"
download.file(url, destfile = "blish_covid.seu.rds")
```
We use the single cell RNA-sequencing data on Peripheral blood mononuclear cells (PBMC) from COVID patients and healthy controls, choose cell type B and genes with top 5000 highest expression levels.  
```R
pbmc = readRDS('blish_covid.seu.rds')
# Use the original UMI counts stored in Assay 'RNA'
DefaultAssay(pbmc) = 'RNA'
pbmc.updated = UpdateSeuratObject(object = pbmc) 
# select cell type B, genes with top 5000 highest expression levels
pbmc_B = pbmc.updated[,pbmc.updated$cell.type.coarse %in% 'B']
mean_exp = rowMeans(pbmc_B@assays$RNA@counts/pbmc_B$nCount_RNA)
genes_selected = names(sort.int(mean_exp, decreasing = T))[1:5000]
pbmc_B_healthy = pbmc_B[, pbmc_B$Status == "Healthy"]
rm(pbmc,pbmc_B,pbmc.updated)
```
## 2. specify parameters for simulation

We specify $\mu_j,\sigma_{jj},s_i,{\bf R},j=1...p,i=1...n$ from PBMC scRNA data, simulate n=200 cells and p=100 genes

We apply CS-CORE to estimate R from real data( pbmc_B_health )
```R
CSCORE_result = CSCORE(pbmc_B_healthy, genes = genes_selected[1:100])
```
```R
library(Matrix)
#set co-expression estimates with absolute values less than 0.5 to 0 to encourage sparsity
R = CSCORE_result$est
R[abs(R)<0.5] = 0

#Project R onto positive definite matrices"
R = nearPD(R,corr = T,base.matrix = T)$mat 
print(R[1:5,1:5])
```

Then we estimate $\mu$, $\sigma_{jj}$ and sequence depth $s_i$, $\mu$, $\sigma_{jj}$ are estimated from the mean and variance of real data, $s_i$ are sampled from the sequencing depths of real data. Parameters of Gamma distribution $\alpha_j, \beta_j$ are specified via relationship $\mu_j=\frac{\alpha_j}{\beta_j},\sigma^2_{jj}=\frac{\alpha_j}{\beta_j^2}$.  
```R
data = t(pbmc_B_healthy@assays$RNA@counts)
data = data[,match(genes_selected[1:100], colnames(data)), drop = F]
#seq depth s
seq_depth = rowSums(data)
# mu,sigma: estimates for the top p highly expressed genes
data = data/seq_depth
mu = apply(data,2,mean)
sigma_2 = apply(data,2,var)
# alpha, beta for gamma
beta = mu/sigma_2
alpha = mu*beta
```

## 3. simulation given R and $\alpha_j,\beta_j$.

generate n = 200 cells, p = 100 genes

Steps:
1. generate $(v_{i1},\cdots,v_{ip}) \sim N_p(0,R)$

2. generate $(z_{i1},\cdots,z_{ip})$ by $z_{ij} = F_j^{-1}(\Phi(v_{ij})), F_j \text{ is the CDF of Gamma }(\alpha_j,\beta_j)\implies z_{ij} \sim \text{ Gamma } (\alpha_j,\beta_j)$.

3. sample n $s_i$ from real sequence depth.

4. generate $x_{ij}|z_{ij} \sim \text{ Poisson }(s_iz_{ij}), \text{ marginally } x_{ij}\text{ is negative binomial}$

```R
library(MASS)
n = 200
v = mvrnorm(n,mu = rep(0,nrow(R)),Sigma = R)
temp = pnorm(v) #\Phi(v_ij)
temp = rbind(alpha,beta,temp)
```
```R
# define F_j inverse
F_j_inverse = function(x){
  alpha = x[1]
  beta = x[2]
  z = qgamma(x[-(1:2)], shape = alpha, rate = beta)
  return(z)
}
# z_ij = F_j^{-1}(\Phi(v_{ij}))
z = apply(temp,2,F_j_inverse)
```

$x_{ij}|z_{ij} \sim \text{ Poisson }(s_iz_{ij})$
```R
# sample n=200 sequence depth
s = sample(seq_depth,200,replace = T)
# generate count matrix X
temp = z*s
count_matrix = apply(temp,2,function(lambda) rpois(n,lambda))
```
We will apply two estimators on the simulated data count_matrix.

## 4. Estimate

4.1 method: cscore
```R
X = count_matrix
R.cscore = CSCORE_IRLS(X,seq_depth = rowSums(X))$est
```

4.2 method: rank-based estimator

1. Compute Kendall's $\tau$
```R
library(pcaPP)
X = count_matrix
X_s = rowSums(X)
X_s[X_s==0]=1
X = X/X_s
tau = cor.fk(as.matrix(X))
tau[is.nan(tau)] = 0
diag(tau) = 1
```
Estimate $\hat \Delta_j=\Phi^{-1} \{\sum_{i=1}^{n} I( X_{ij} = 0)/n \}$
```R
n = nrow(X)
delta = qnorm(colSums(X==0)/n) 
```
$F_{TT}^{-1}$ does not have closed form, so we estimate $\hat R$ elementwise by solving $\hat R_{jk}={\rm arg\,min}_{r}\{F(r)-\hat \tau_{jk}\}^2$
```R
library(mvtnorm)

F_TT = function(sigma,deltaj,deltak) {
  cor4a = matrix(c(1, 0, 1/sqrt(2), -sigma/sqrt(2),
                  0, 1, -sigma/sqrt(2), 1/sqrt(2),
                  1/sqrt(2), -sigma/sqrt(2), 1, -sigma,
                  -sigma/sqrt(2), 1/sqrt(2), -sigma, 1),
                nrow=4, byrow = T)
  cor4b = matrix(c(1, sigma, 1/sqrt(2), sigma/sqrt(2),
                  sigma, 1, sigma/sqrt(2), 1/sqrt(2),
                  1/sqrt(2), sigma/sqrt(2), 1, sigma,
                  sigma/sqrt(2), 1/sqrt(2), sigma, 1),
                nrow=4, byrow = T)
  r = -2*pmvnorm(-Inf, c(-deltaj,-deltak,0,0), mean = rep(0,4), corr = cor4a) + 2*pmvnorm(-Inf, c(-deltaj,-deltak,0,0), mean = rep(0,4), corr = cor4b)
  return(r)
}

upper_indices = which(upper.tri(tau),arr.ind = T)

time_taken = system.time({
  R.upper = mapply(function(j,k){
  temp = optimize(f = function(r){(F_TT(r,delta[j],delta[k])-tau[j,k])^2},interval = c(-1,1));temp$minimum}, upper_indices[,1],upper_indices[,2])
})

R.rank = matrix(0, nrow = nrow(tau), ncol = ncol(tau))
R.rank[upper_indices] = R.upper
R.rank = R.rank + t(R.rank)
diag(R.rank) = 1

print(R.rank[1:5,1:5])
```
## 5. result
```R
# true correltation is R
mean(abs(R-R.cscore))
mean(abs(R-R.rank))
mean(abs(R-tau)) 
```

