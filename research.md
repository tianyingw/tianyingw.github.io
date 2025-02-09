---
layout: page
title: Overview
---

<p align="justify">
My research focuses on developing statistical methods to address fundamental data challenges, including heterogeneity, measurement errors, missingness, and zero-inflation. These challenges arise in diverse domains such as genomics, epidemiology, and electronic health records, where conventional statistical models often fall short. To tackle these issues, I leverage and extend methodologies in quantile regression, machine learning, and debiasing techniques from measurement error analysis. My goal is to create robust, interpretable, and computationally efficient approaches that improve inference and prediction in complex data environments.
</p> 

<p align="justify">
<ins>underline</ins> indicates a student working under my (co)supervision, with <sup><span>&#9830;</span></sup> denoting an undergraduate student mentee; <span>&#x2709;</span> indicates the corresponding author.
</p>

### Understanding Heterogeneous Data with Quantile Regression 
<p align="justify">
Real-world data often exhibit complex, nonlinear, and heterogeneous relationships that traditional mean-based methods fail to capture. I develop and extend quantile regression techniques to model variability across different parts of the data distribution, enabling more insights into heterogeneous associations. This is particularly relevant in applications such as personalized medicine and socioeconomic studies, where responses vary across subpopulations.
</p>

- **Wang, T.<span>&#x2709;</span>**, Ma, Y, and Wei, Y. (2025+). _"Time-varying Quantile Regression with Multi-outcome Latent Groups"_, under review.
- <ins>Jiang, R.</ins>, and **Wang, T.<span>&#x2709;</span>** (2025+). _"A Minimax Optimal Quantile Rank Score Test"_, under review.
- Liu, Y. and **Wang, T.<span>&#x2709;</span>** (2025+). _"A powerful transformation of quantitative responses for biobank-scale association studies"_, under review.
- **Wang, T.<span>&#x2709;</span>**, Ionita-Laza, I., and Wei, Y. (2024). ["A unified quantile framework for nonlinear heterogeneous transcriptome-wide associations"](https://arxiv.org/abs/2207.12081), **_Annals of Applied Statistics_**, accepted.
- Wang, C., **Wang, T.**, Kiryluk, K., Wei, Y., Aschard, H., and Ionita-Laza, I. (2024). ["Genome-wide discovery for biomarkers using quantile regression at biobank scale"](https://www.nature.com/articles/s41467-024-50726-x), Nature Communications, 15 (1), 6460.
- **Wang, T.<span>&#x2709;</span>**, Ionita-Laza, I., and Wei, Y. (2022). ["Integrated Quantile RAnk Test (iQRAT) for gene-level associations"](https://projecteuclid.org/journals/annals-of-applied-statistics/volume-16/issue-3/Integrated-Quantile-RAnk-Test-iQRAT-for-gene-level-associations/10.1214/21-AOAS1548.short). **_Annals of Applied Statistics_**, 16 (3), 1423 - 1444. 
- **Wang, T.**, Ling, W., Plantinga, A., Wu, M., and Zhan, X. (2022). ["Testing microbiome association using integrated quantile regression models"](https://academic.oup.com/bioinformatics/advance-article-abstract/doi/10.1093/bioinformatics/btab668/6374494). **_Bioinformatics_**, 38(2), 419-425. 


### Correcting Bias in Complex Data with Measurement Errors
<p align="justify">
Many datasets contain errors due to mismeasurement, rounding, or systematic bias, particularly in high-dimensional, count, and compositional data. I work on error-in-variables models, de-biasing techniques, and correction methods that enhance the reliability of statistical inference. My approaches improve estimation and hypothesis testing in settings like nutritional epidemiology and biomedical research, where measurement errors can significantly distort conclusions.
</p>

- <ins>Li, Z.</ins>, and **Wang, T.<span>&#x2709;</span>** (2025+). _"Tree-aggregation of high-dimensional compositional data subject to measurement errors"_, under review.
- <ins>Zhao, H.</ins>, and **Wang, T.<span>&#x2709;</span>** (2025+). _"A simulation-free extrapolation method for misspecified models with errors-in-variables"_, under review.
- <ins>Zhao, H.</ins>, and **Wang, T.<span>&#x2709;</span>** (2024). _["A high-dimensional calibration method for log-contrast models subject to measurement errors"](https://academic.oup.com/biometrics/article/80/4/ujae153/7925418)_, **_Biometrics_**, accepted.
- Li, Y., **Wang, T.<span>&#x2709;</span>**, Yan, J., and Zhang, X. (2024). _"Improved Optimal Fingerprinting Based on Estimating Equations Reaffirms Anthropogenic Effect on Global Warming"_,  **_Journal of Climate_**, accepted.
- Zhou, S., Pati, D., **Wang, T.**, Yang, Y., and Carroll, R. J. (2023). ["Gaussian Processes with Errors in Variables: theory and computation"](https://jmlr.org/papers/volume24/21-1480/21-1480.pdf), _Journal of Machine Learning Research_, 24, 1-53.
- <ins>Lau, Y.</ins>, **Wang, T.<span>&#x2709;</span>**, Yan, J., and Zhang, X. (2023). ["Extreme Value Modeling with Errors-in-Variables in Detection and Attribution of Changes in Climate Extremes"](https://doi.org/10.1007/s11222-023-10290-8), _Statistics and Computing_, 33 (6), 125.
- <ins>Ma, S.</ins>, **Wang, T.<span>&#x2709;</span>**, Yan, J., and Zhang, X. (2023). ["Optimal Fingerprinting with Estimating Equations"](https://journals.ametsoc.org/configurable/content/journals$002fclim$002faop$002fJCLI-D-22-0681.1$002fJCLI-D-22-0681.1.xml?t:ac=journals%24002fclim%24002faop%24002fJCLI-D-22-0681.1%24002fJCLI-D-22-0681.1.xml), _Journal of Climate_, 36(20), 7109-7122.
- <ins>Jiang, R.**<sup><span>&#9830;</span></sup>**</ins>, Zhan, X.<span>&#x2709;</span>, and **Wang, T.<span>&#x2709;</span>** (2023). ["A Flexible Zero-Inflated Poisson-Gamma Model with Application to Microbiome Read Count Data"](https://www.tandfonline.com/doi/full/10.1080/01621459.2022.2151447), _Journal of the American Statistical Association_, 118 (542), 792 - 804. 
- Blas Achic, B.<sup><span>&#9839;</span></sup>, **Wang, T.<sup><span>&#9839;</span></sup>** , Su, Y., Kipnis, V., Dodd, K., and Carroll, R. J. (2018). _"Categorizing a Continuous Predictor Subject to Measurement Error"_. _Electronic Journal of Statistics_, Vol. 12, No. 2, 4032-4056. **( <sup><span>&#9839;</span></sup> joint first authors)**. 

### Advancing Learning Methods for Missing and Zero-Inflated Data
<p align="justify">
Missing values and zero inflation are prevalent in fields such as clinical trials, microbiome studies, and financial data. I develop statistical and machine learning approaches, including transfer learning and imputation techniques, to mitigate bias and improve predictive performance. By designing methods that adapt to data sparsity and structural zeros, I aim to enhance inference in cases where traditional methods struggle with loss of information.
</p>

- <ins>Zhao, H.</ins>, and **Wang, T.<span>&#x2709;</span>** (2025+). _"Generalizing Transfer Learning: A Flexible Doubly Robust Estimation Approach for Missing Data"_, under review.
- <ins>Zhao, H.</ins>, and **Wang, T.<span>&#x2709;</span>** (2025+). _"Doubly robust augmented model transfer inference with completely missing covariates"_, under review.
- <ins>Wang, Z.</ins>, and **Wang, T.<span>&#x2709;</span>** (2024). _"A Semiparametric Quantile Single-Index Model for Zero-Inflated Outcomes"_, **Statistica Sinica**, accepted.
- **Wang, T.<span>&#x2709;</span>**, Zhang, W., and Wei, Y. (2024). ["ZIKQ: An innovative centile chart method for utilizing natural history data in rare disease clinical development"](https://www3.stat.sinica.edu.tw/ss_newpaper/SS-2023-0107_na.pdf), _Statistica Sinica_, accepted.
- <ins>Wang, Z.</ins>, Ling, W. and **Wang, T.<span>&#x2709;</span>** (2024). _"A Semiparametric Quantile Regression Rank Score Test for Zero-inflated Data"_, under review.

### Other topics
<p align="justify">
I am also interested in a broad range of research topics, such as high-dimensional statistics and case-control studies.
</p>

- <ins>Wang, Y.</ins>, and **Wang, T.<span>&#x2709;</span>** (2025+). _"Multi-Group Quadratic Discriminant Analysis via Projection"_, under review.
- **Wang, T.**, Liu, J., and Wu, A. (2024). ["Semiparametric Analysis in Case-Control Studies for Gene-Environment Independent Models: Bibliographical Connections and Extensions"], _Journal of Data Science_, accepted.
- Ma, S. and **Wang, T.<span>&#x2709;</span>** (2023). "The optimal pre-post allocation for randomized clinical trials". _BMC Medical Research Methodology_,  23:72 doi: 10.1186/s12874-023-01893-w.
- **Wang, T.<span>&#x2709;</span>** and Asher, A. (2021). "Improved Semiparametric Analysis of Polygenic Gene-Environment Interactions in Case-Control Studies". _Statistics in Biosciences_, 13, 386--401.
- Gaynanova, I. and **Wang, T.** (2019). "Sparse quadratic classification rules via linear dimension reduction". _Journal of Multivariate Analysis_, 169, 278--299.



_**Please check [here](https://tianyingw.github.io/publications/) for more of my publications.**_



[Research opportunities](https://tianyingw.github.io/openings/) are open to highly motivated students. Interested individuals are encouraged to reach out for more details. 

