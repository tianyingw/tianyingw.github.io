---
layout: page
title: Construct co-expression network for single-cell data
---
Note: This is a project summary created by Mujin Zhou from Tsinghua University under the supervision of Tianying Wang.


## Introduction

Inference of gene co-expression is pivotal for our understanding of biological functions and gene regulations. For scRNA-seq data, the expression level of a specific gene is measured through the observed UMI (unique molecular identifier) count for this gene, and the sequencing depth of a cell is the sum of UMI counts across all genes. The gene co-expression is measured by correlations of UMI counts.

This document aims to describe the process of inferring gene co-expression with a rank-based estimator based on a latent Gaussian copula model and conduct a simulation study that assesses the performance of estimators. To construct co-expression networks, we first review the method of [CS-CORE](https://www.nature.com/articles/s41467-023-40503-7) (cell-type-specific co-expressions)[^fn1]. CS-CORE models the underlying expression levels as latent variables, linked to the observed UMI counts through a Poisson measurement model depending on the underlying expression levels and sequencing depth. Under this model, CS-CORE implements an iteratively re-weighted least squares approach for estimating the true correlations between underlying expression levels. Building upon the CS-CORE framework, we incorporate the semiparametric approach proposed by [Grace Yoon et al. (2020)](https://academic.oup.com/biomet/article/107/3/609/5820553?login=true)[^fn2], which models the latent variables with a Gaussian copula and use a rank-based estimator for correlation estimation.

The observed UMI counts for $p$ genes of cell $i, i=1,\cdots,n$ from $n$ cells is denoted by $(x\_{i1},\cdots,x\_{ip})$. ${s}\_{i}=\mathop{\sum }\nolimits\_{j=1}^{p}{x}\_{ij}$ denotes the sequencing depth of cell $i$, which is the sum of UMI counts across $p$ genes. $(z\_{i1},\cdots,z\_{ip})$ denote the underlying expression levels from $p$ genes in cell $i$, defined to be the UMI counts from each gene relative to the sequencing depth $s\_i$. Assume that:
$$(z\_{i1},...,z\_{ip}) \sim F\_p({\bf \mu,\Sigma}),x\_{ij}|z\_{ij}\sim \text{Poisson}(s\_iz\_{ij}),$$
where $F\_p(\bf \mu,\Sigma)$ is an unknown nonnegative $p$-variate distribution with mean vector $\mu=(\mu\_1,\cdots,\mu\_p)$, $\sum\_{j=1}^p \mu\_j = 1$ and covariance matrix ${\bf\Sigma}  = (\sigma\_{jj'})\_{p \times p}$, the element in row $j$ and column $j'$ being $\sigma\_{jj'}$. Here, $x\_{ij}$ is the UMI count of gene $j$ in cell $i$, assumed to follow a Poisson measurement model depending on the underlying expression level $z\_{ij}$ and sequencing depth $s\_i$. This Poisson measurement model explicitly accounts for the sequencing depths so that the gene co-expressions measured by ${\bf\Sigma} = (\sigma\_{jj'})\_{p \times p}$, the covariance of $(z\_{i1},...,z\_{ip})$, is not biased by sequencing depths.

## Methods
CS-CORE uses a moment-based iteratively reweighted least squares approach to estimate the covariance $\Sigma$. Given $\{x\_{i1},...,x\_{ip}\}\_i^n$ and $\{s\_i\}\_i^n$, under the model in assumptions, $E({x}\_{ij})={s}\_{i}{\mu }\_{j}, {{{{{{{\rm{Var}}}}}}}}({x}\_{ij})=E[{({x}\_{ij}-{s}\_{i}{\mu }\_{j})}^{2}]={s}\_{i}{\mu }\_{j}+{s}\_{i}^{2}{\sigma }\_{jj}, E[({x}\_{ij}-{s}\_{i}{\mu }\_{j})({x}\_{i{j}^{' }}-{s}\_{i}{\mu }\_{{j}^{' }})]={s}\_{i}^{2}{\sigma }\_{j{j}^{' }}$, so the following set of regression equations hold: 
```math
\begin{array}{rlr}
&{x}_{ij}={s}_{i}{\mu }_{j}+{\epsilon }_{ij}, &\\ 
&{({x}_{ij}-{s}_{i}{\mu }_{j})}^{2}={s}_{i}{\mu }_{j}+{s}_{i}^{2}{\sigma }_{jj}+{\eta }_{ij}, \\ 
&({x}_{ij}-{s}_{i}{\mu }_{j})({x}_{i{j}^{' }}-{s}_{i}{\mu }_{{j}^{' }})={s}_{i}^{2}{\sigma }_{j{j}^{' }}+{\xi }_{ij{j}^{' }},
\end{array}
```
where ${\epsilon }\_{ij}, {\eta }\_{ij}, {\xi }\_{ij{j}^{' }}$ are independent and mean-zero error variables for all $i, j, j'$.  
Then $\mu\_j, \sigma\_{jj}, \sigma\_{jj'}$ are estimated by weighted least squares:
```math
\begin{aligned}
    \hat \mu_j &= {\min }_{\mu }\mathop{\sum }\nolimits_{i=1}^{n}{w}_{ij}{({x}_{ij}-{s}_{i}\mu )}^{2}\\
    \hat \sigma_{jj} &= {\min }_{\sigma }\mathop{\sum }\nolimits_{i=1}^{n}{h}_{ij}{[{({x}_{ij}-{s}_{i}{\hat{\mu }}_{j})}^{2}-{s}_{i}{\hat{\mu }}_{j}-{s}_{i}^{2}\sigma ]}^{2}\\
    \hat \sigma_{jj'} &= {\min }_{\sigma }\mathop{\sum }\nolimits_{i=1}^{n}{g}_{ij{j}^{' }}{[({x}_{ij}-{s}_{i}{\hat{\mu }}_{j})({x}_{i{j}^{' }}-{s}_{i}{\hat{\mu }}_{{j}^{' }})-{s}_{i}^{2}\sigma ]}^{2}\\
\end{aligned}
```
where ${w}\_{ij}, h\_{ij}, g\_{ijj'}$ are the weights. In the interative process, the weights are updated: ${w}\_{ij}=1/{{{{{{{\rm{Var}}}}}}}}({\epsilon }\_{ij})=1/({s}\_{i}{\mu }\_{j}+{s}\_{i}^{2}{\sigma }\_{jj})$, ${h}\_{ij}={w}\_{ij}^{2}$ and ${g}\_{ij{j}^{' }}={w}\_{ij}{w}\_{i{j}^{' }}$. Finally we have $\hat\mu\_j, {\bf\hat\Sigma}=(\hat\sigma\_{jk})\_{p \times p}$, leading to the estimation of the correlation matrix $\bf \hat R$, whose element in row $j$ and column $k$ is ${\hat{\rho }}\_{jk}={\hat{\sigma }}\_{jk}/\sqrt{{\hat{\sigma }}\_{jj}{\hat{\sigma }}\_{kk}}$. We called the estimator R.cscore.

The proposed model in CS-CORE does not impose distributional assumptions on the underlying expression levels, its distribution being an unknown nonnegative $p$-variate distribution, $(z\_{i1},\cdots,z\_{ip}) \sim F\_p(\mu, {\bf \Sigma})$. We reviewed Grace Yoon's paper and adopted its approach, modeling latent variables with a Gaussian copula. The assumption is that the Gaussian copula can be transformed into the distribution of observed count data through unknown monotonic transformations, and due to the invariance of Kendall's $\tau$, the measure of correlation based on ranks, under monotonic transformations, a bridge function can link the Kendall's $\tau$ of the observed data to the correlation matrix of the latent Gaussian copula. We justify applying this assumption to observed UMI counts, that is, the existence of monotonic functions that transform the Gaussian distribution into the Poisson measurement model.

Assume that a truncated Gaussian copula underlies ($z\_{i1},...,z\_{ip}$), where $(z\_{i1}, \cdots, z
\_{ip})$ is the positive truncation of a continuous vector $(u\_{i1},\cdots,u\_{ip})$, that is, there exist $(u\_{i1},\cdots,u\_{ip})$, a set of monotonically increasing functions $f = (f\_j)\_{j=1}^p$ and a vector of constants ${\bf C} = (C\_1,\cdots C\_p)$, $f\_j(u\_{ij})$ denoted as $v\_{ij}$, such that:
```math
\begin{aligned}
    &z_{ij} = I(u_{ij}>C_j)u_{ij}\\
    &(v_{i1},\cdots,v_{ip}) = (f_1(u_{i1}),\cdots,f_p(u_{ip}))\\
    &(v_{i1},\cdots,v_{ip}) \sim N_p(0,{\bf R}),R_{jj}=1\\
\end{aligned}
```
Our goal is to estimate the latent correlation matrix ${\bf R}$, though transformations $f = (f\_j)\_{j=1}^p$ are unknown so latent variables $(v\_{i1},\cdots,v\_{ip})$ are not directly observable. ${\bf R}$ can be connected to the observed data by two steps: 1. Kendall's $\tau$ of the observed $(z\_{i1},\cdots,z\_{ip})$ and that of latent Gaussian copula $(v\_{i1},\cdots,v\_{ip})$ are the same, so it bypasses the unknown transformations $f = (f\_j)\_{j=1}^p$; 2. ${\bf R}$, the correlation matrix of $(v\_{i1},\cdots,v\_{ip})$, can be linked to its Kendall's $\tau$ by a bridge function, whose  explicit formulas for truncated data are derived in Grace Yoon's paper. 

First, we demonstrate the invariance of Kendall's $\tau$. Given the observed data of the gene pair $(z\_{ij},z\_{ik}), i=1,\cdots,n$, the sampled Kendall's $\tau$ is defined as $\hat\tau\_{jk} =\frac{2}{n(n-1)}\sum\_{1\le i<i'\le n} sign(z\_{ij}-z\_{i'j})sign(z\_{ik}-z\_{i'k})$, and the population Kendall's $\tau$ is defined as 
$\tau\_{jk}=E(\hat\tau\_{jk})$.  
Denote $\Delta\_j = f\_j(C\_j), j=1,\cdots,p$, because for any monotonic $f\_j()$, 
```math
sign(z_{ij}-z_{i'j}) = sign(I(v_{ij}>\Delta_j)v_{ij}-I(v_{i'j}>\Delta_j)v_{i'j})
```
, $\tau\_{jk}$ of $(z\_{ij},z\_{ik})$ is equivalent to $\tau\_{jk}$ of $(I(v\_{ij}>\Delta\_j)v\_{ij},I(v\_{ik}>\Delta\_k)v\_{ik})$, depending only on $v\_{ij}, v\_{ik}, \Delta\_j, \Delta\_k$. $\tau\_{jk}$ is a function of ${\bf R}\_{jk}$ independent of $(f\_j)\_{j=1}^p$, and we denote this function as bridge function $\tau\_{jk} = F({\bf R}\_{jk};\Delta\_j,\Delta\_k)$ with parameters $\Delta\_j,\Delta\_k$.

The bridge function establishes the connection between the latent correlation $\bf R$ and the population Kendall's $\tau$. The explicit form of the bridge function F is derived in Grace Yoon's paper. That is, $F({\bf R}\_{jk};\Delta\_j, \Delta\_k) = -2 \Phi\_4 (-\Delta\_j, -\Delta\_k, 0,0; \Sigma\_{4a}) + 2 \Phi\_4 (-\Delta\_j, -\Delta\_k, 0,0; \Sigma\_{4b})$, with 
```math
\begin{aligned}
\Sigma_{4a} & = \begin{pmatrix}
1 \; & \; 0 \; &\; 1/\sqrt{2} \; & \; -{\bf R}_{jk}/\sqrt{2}\\
0\; &\; 1 \; &\; -{\bf R}_{jk}/\sqrt{2}\; & \; 1/\sqrt{2}\\
1/\sqrt{2}\; &\; -{\bf R}_{jk}/\sqrt{2} \; &\; 1\; & \; -{\bf R}_{jk}\\
-{\bf R}_{jk}/\sqrt{2}\; & \; 1/\sqrt{2}\; &\; -{\bf R}_{jk}\; &\; 1
\end{pmatrix}\!,
\\
\Sigma_{4b} & = \begin{pmatrix}
1 \; & \; {\bf R}_ {jk}\; &\; 1/\sqrt{2}\; & \;{\bf R}_ {jk}/\sqrt{2}\\
{\bf R}_ {jk}\; &\; 1\; & \;{\bf R}_ {jk}/\sqrt{2}\; &\; 1/\sqrt{2}\\
1/\sqrt{2}\; & \;{\bf R}_ {jk}/\sqrt{2}\; & \;1\; &\; {\bf R}_ {jk}\\
{\bf R}_ {jk}/\sqrt{2}\; & \;1/\sqrt{2}\; & \; {\bf R}_ {jk}\; & \;1
\end{pmatrix}\!.
\end{aligned}
```
The derivation of the bridge function involves plugging the expression $sign(x) = 2I(x > 0) - 1$ into the definition of $\tau\_{jk}$. This allows us to rewrite it as the expectation of indicator functions, and then the joint probability of multivariate normal distribution. Ultimately, this can be rewritten as cumulative normal distribution functions.

For example, without loss of generality we set j = 1 and k = 2, $(v\_{i1},v\_{i2}),(v\_{i'1},v\_{i'2})$ as $(v\_1,v\_2),(v'\_1,v'\_2)$. 
```math
\begin{aligned}
    \tau_{jk} = &-2E[I(v_1\leq\Delta_1,v'_2-v_2<0)]+2E[I(v'_1\leq\Delta_1,v'_2-v_2<0)]\\
    &+E[I(v_1>\Delta_1,v'_1>\Delta_1)sign(v_1-v'_1)sign(v_2-v'_2)]
\end{aligned}
```
The last term can be written as joint probability
```math
\begin{aligned}
    &P(v_1>\Delta_1,v'_1>\Delta_1,v_1-v'_1>0,v_2-v'_2>0)\\
    +&P(v_1>\Delta_1,v'_1>\Delta_1,v_1-v'_1<0,v_2-v'_2<0)\\
    -&P(v_1>\Delta_1,v'_1>\Delta_1,v_1-v'_1>0,v_2-v'_2<0)\\
    -&P(v_1>\Delta_1,v'_1>\Delta_1,v_1-v'_1<0,v_2-v'_2>0)\\
\end{aligned}
```
And then because $(v\_1,v'\_1,v\_1-v'\_1,v\_2-v'\_2)$ follows a multivariate distribution, we can compute the covariance matrix and rewrite it as CDF $\Phi\_4(\cdot, \cdot, \cdot, \cdot;\Sigma)$.  
Because $\Delta\_j = f\_j(C\_j)$ is unknown in practice, we used an estimator. Based on the moment equation ${E} \{I(z\_{ij}>0) \} = {\rm pr} (z\_{ij}>0) = {\rm pr} \{f\_j(u\_{ij})>\Delta\_j\} = 1-\Phi(\Delta\_j)$, we use $\hat\Delta\_j=\Phi^{-1}(\sum\_{i=1}^n I(z\_{ij}=0)/n)$.

The estimation procedure of $R$ given the observed data matrix ${\rm X}\in R^{n \times p}$:  
Step 1: $s\_i = \sum\_{j=1}^p E(x\_{ij})$, estimate $\hat s\_i = \sum\_{j=1}^p x\_{ij}$  
Step 2: $\hat z\_{ij} = x\_{ij}/\hat s\_i$  
Step 3: estimate $\hat \tau\_{jk}$ from $\hat Z = (\hat z\_{ij})\_{n \times p}$  
Step 4: estimate $\hat \Delta\_j = \Phi^{-1}(\sum\_{i=1}^n I(\hat z\_{ij}=0)/n)$  
Step 5: estimate R, $\hat R\_{jk} = F^{-1}(\hat \tau\_{jk})$ with parameters $\hat\Delta\_j,\hat\Delta\_k$  
We call the rank-based estimator R.rank.  

## Simulation Study  
To validate our approach, we conduct a simulation study that assesses the performance of our estimators under various conditions. We followed the simulation method in Chang Su's paper. We specified the distribution of true expression level $z\_{ij}$ to be Gamma distribution, marginally $z\_{ij} \sim \text{ Gamma }(\alpha\_j,\beta\_j), \mu\_j = \alpha\_j/\beta\_j, \sigma\_{jj} = \alpha\_j/\beta\_j^2$, where $\mu\_j$ and $\sigma\_{jj}$ correspond to the marginal mean and variance in assumption $F\_p(\mu, {\bf \Sigma})$. Conditional on $z\_{ij}$, we simulated counts $x\_{ij} \sim \text{Poisson}(s\_iz\_{ij})$. We obtain $s\_i,\mu\_j,\sigma\_{jj}$ from the sequencing depths, mean and variance of real data, and then obtain $\alpha\_j,\beta\_j$ from $\mu\_j = \alpha\_j/\beta\_j, \sigma\_{jj} = \alpha\_j/\beta\_j^2$.  
Next, given a correlation matrix $\bf R^\*$, we adopted a Gaussian copula to generate correlated Gamma random variables: $(v\_{i1},...,v\_{ip}) \sim N(0,\bf R^\*)$ and then generate ${z}\_{ij}={F}\_{j}^{-1}({{\Phi }}({v}\_{ij}))$ where $F\_j$ is the CDF of $\text{ Gamma }(\alpha\_j,\beta\_j)$, $\bf R^*$ is estimated from real data by Cscore.  
$(z\_{i1},...,z\_{ip}) \sim F\_p(\mu,\Sigma)$, where $\sigma\_{jk} = cov({F}\_{j}^{-1}({{\Phi }}({v}\_{ij})),{F}\_{k}^{-1}({{\Phi }}({v}\_{ik})))$  
For details and implementation of simulation in R, see more information [here]().


[^fn1]: Su, C., Xu, Z., Shan, X. et al. Cell-type-specific co-expression inference from single cell RNA-sequencing data. Nat Commun 14, 4846 (2023).

[^fn2]: Grace Yoon, Raymond J Carroll, Irina Gaynanova, Sparse semiparametric canonical correlation analysis for data of mixed types, Biometrika, Volume 107, Issue 3, September 2020, Pages 609–625.

