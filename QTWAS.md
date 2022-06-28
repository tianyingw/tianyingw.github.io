---
layout: page
title: QTWAS
bibliography: QTWAS.bib
---

## A Unified Quantile Framework for Transcriptome-Wide Association Analysis

<img align="center" src="/img/flowchart_new.jpg" alt="" width="800">

### Methodology

  - Please see the manuscript ["A Unified Quantile Framework reveals nonlinear heterogeneous transcriptome-wide associations"](http://www.columbia.edu/~ii2135/QTWAS.pdf) for more details.

### Software

  We developed software tools based on R: [_QTWAS_](https://github.com/tianyingw/QTWAS) for training gene expression model on based on GTEx data. Please see the Github page for more details.
  

### Models

We provide pre-trained QTWAS models per gene for 49 tissues in [GTEx v8](https://gtexportal.org/home/). _R scores_ for evaluating imputation accuracy are also provided for each model.

  - Download all the QTWAS models [_here_](). In each database file, we provide the information for:
    - estimated beta at selected SNPs, indexed by _rsid_ and _gene ensemble ID_. _interval_ represents the quantile region of gene expression, i.e., <img src="https://render.githubusercontent.com/render/math?math=A_k">. 
    - covariance matrix of SNPs in the imputation models, indexed by _rsid_ and _gene ensemble ID_.
  
    Code to extract the information:
    ```
    driver <- dbDriver('SQLite')
    conn <- dbConnect(drv = driver, file.name) #use the file you want to extract for file.name
    mytable.beta <- dbReadTable(conn,"beta")
    mytable.cov_mat <- dbReadTable(conn,"cov_mat")
    dbDisconnect(conn)
    ```
  - Download R scores for each model [_here_]()

### Results

#### Ten psychiatric/disorder diseases 
    
  Here we provide QTWAS results on the summary statistics from ten GWAS studies on brain disorders, including five neuropsychiatric traits: schizophrenia (SCZ[^fn1]), attention-deficit/hyperactivity disorder (ADHD[^fn2]), bipolar disorder (BD[^fn3]), autism spectrum disorder (ASD[^fn4]) and major depressive disorder (MDD[^fn5]); and four neurodegenerative traits: Alzheimer's disease (AD\_Kunkle[^fn6] and AD\_Jansen[^fn7]), Parkinson's disease (PD[^fn8]), multiple sclerosis (MS[^fn9]) and amyotrophic lateral sclerosis (ALS[^fn10]). 

  - Download [Manhattan plots](https://www.dropbox.com/sh/ksva8yexsud9on6/AADnj7RcLC0TH4xvLlVea_ZHa?dl=0) per triat (multi-tissue results based on 13 brain tissues)
    
  - Download [QQ plots](https://www.dropbox.com/sh/omgvs4hxzlcpik8/AABqMYBiFGSzhqwFvvY5dPjZa?dl=0) per tissue per trait for all 49 tissues
  
  - Download [Significant genes](https://www.dropbox.com/sh/qd21drdjdcz3t5h/AADGM3JwZ6SkkG9syIJDaXHIa?dl=0) per tissue per trait for all 49 tissues
    
  - Download [QTWAS p values for all genes]() per tissues per trait for all 49 tissues
    
#### 797 UK Biobank traits
   
   We also provide QTWAS results on [797 UK Biobank  continuous phenotypes](https://pan.ukbb.broadinstitute.org) with their summary statistics on 28 million imputed variants. We provide phenome-wide results for genes, genome-wide gene-based results for each trait with respect to all 49 tissues separately.
   
  - Download [QTWAS p values for all genes]() per tissues per trait for all 49 tissues

### References

[^fn1]: Pardiiñas, A. F., Holmans, P., Pocklington, A. J., Escott-Price, V., Ripke, S., Carrera, N., Legge, S. E., Bishop, S., Cameron, D., Hamshere, M. L., et     al. (2018). Common schizophrenia alleles are enriched in mutation-intolerant genes and in regions under strong background selection. Nature genetics, 50, 381–389.

[^fn2]: Demontis, D., Walters, R. K., Martin, J., Mattheisen, M., Als, T. D., Agerbo, E., Baldursson, G., Belliveau, R., Bybjerg-Grauholm, J., Bækvad-Hansen, M., et al. (2019). Discovery of the first genome-wide significant risk loci for attention deficit/hyperactivity disorder. Nature genetics, 51, 63–75.

[^fn3]: Sarlus, H., Heneka, M. T., et al. (2017). Microglia in alzheimer’s disease. The Journal of clinical investigation, 127, 3240–3249.

[^fn4]: Grove, J., Ripke, S., Als, T. D., Mattheisen, M., Walters, R. K., Won, H., Pallesen, J., Agerbo, E., Andreassen, O. A., Anney, R., et al. (2019). Identification of common genetic risk variants for autism spectrum disorder. Nature genetics, 51, 431–444.

[^fn5]: Howard, D. M., Adams, M. J., Clarke, T.-K., Hafferty, J. D., Gibson, J., Shirali, M., Cole- man, J. R., Hagenaars, S. P., Ward, J., Wigmore, E. M., et al. (2019). Genome-wide meta-analysis of depression identifies 102 independent variants and highlights the impor- tance of the prefrontal brain regions. Nature neuroscience, 22, 343–352.

[^fn6]: Kunkle, B. W., Grenier-Boley, B., Sims, R., Bis, J. C., Damotte, V., Naj, A. C., Boland, A., Vronskaya, M., Van Der Lee, S. J., Amlie-Wolf, A., et al. (2019). Genetic meta-analysis of diagnosed alzheimer’s disease identifies new risk loci and implicates aβ, tau, immunity and lipid processing. Nature genetics, 51, 414–430.

[^fn7]: Jansen, I. E., Savage, J. E., Watanabe, K., Bryois, J., Williams, D. M., Steinberg, S., Sealock, J., Karlsson, I. K., Ha ̈gg, S., Athanasiu, L., et al. (2019). Genome-wide meta- analysis identifies new loci and functional pathways influencing alzheimer’s disease risk. Nature genetics, 51, 404–413.

[^fn8]: Nalls, M. A., Blauwendraat, C., Vallerga, C. L., Heilbron, K., Bandres-Ciga, S., Chang, D., Tan, M., Kia, D. A., Noyce, A. J., Xue, A., et al. (2019). Identification of novel risk loci, causal insights, and heritable risk for parkinson’s disease: a meta-analysis of genome-wide association studies. The Lancet Neurology, 18, 1091–1102.

[^fn9]: Andlauer, T. F., Buck, D., Antony, G., Bayas, A., Bechmann, L., Berthele, A., Chan, A., Gasperi, C., Gold, R., Graetz, C., et al. (2016). Novel multiple sclerosis susceptibility loci implicated in epigenetic regulation. Science advances, 2, e1501678.

[^fn10]: Van Rheenen, W., Shatunov, A., Dekker, A. M., McLaughlin, R. L., Diekstra, F. P., Pulit, S. L., Van Der Spek, R. A., Vo ̃sa, U., De Jong, S., Robinson, M. R., et al. (2016). Genome-wide association analyses identify new risk variants and the genetic architecture of amyotrophic lateral sclerosis. Nature genetics, 48, 1043–1048.

