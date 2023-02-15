---
layout: page
title: Training
---

<p align="justify">
I have supervised various undergraduate students' research training projects, including statistical and computational methodologies on modeling zero-inflated data, multivariate regression, low-rank approximation, genetic association studies, etc. I am committed to learning what each student needs to succeed and encouraging active learning skills to carry forward. Here are some examples. More on the way! 
</p>

[Research opportunities](https://tianyingw.github.io/openings/) are open to highly motivated students. Interested individuals are encouraged to reach out for more details. 

## Modeling zero-inflated data with error-in-variables

- **Student's name:** Roulan Jiang. (This work was conducted when Roulan was a senior undergraduate student at Tsinghua University from 2021-2022.)

<img align="right" src="/img/Romero_32_violin_pre_Race01.jpg" alt="" width="400">

- **Summary:** In microbiome studies, it is of interest to use a sample from a population of microbes, such as the gut microbiota community, to estimate the population proportion of these taxa. However, due to biases introduced in sampling and preprocessing steps, these observed taxa abundances may not reflect true taxa abundance patterns in the ecosystem. Repeated measures including longitudinal study designs may be potential solutions to mitigate the discrepancy between observed abundances and true underlying abundances. Yet, widely observed zero-inflation and over-dispersion issues can distort downstream statistical analyses aiming to associate taxa abundances with covariates of interest. We propose a Zero-Inflated Poisson Gamma (ZIPG) framework to address the aforementioned challenges. The above figure shows how the estimated differential variability of a taxon in pregnant women changes over age.

- **Related paper:** <ins>Jiang, R.</ins>, Zhan, X.*, and **Wang, T.<b>*</b>** (2022) ["A Flexible Zero-Inflated Poisson-Gamma Model with Application to Microbiome Read Count Data"](https://arxiv.org/pdf/2207.07796.pdf), _Journal of the American Statistical Association_, 1 - 21.

## Quantile TWAS Genome Browser (Shiny app)
- **Student's name:** Weijing Yin. (This work was conducted as a summer project in 2022 when Weijing was a sophomore undergraduate student at Tsinghua University.)

<img align="right" src="/img/shiny.png" alt="" width="400">

- **Summary:** This visualization is based on QTWAS, a quantile regression model for Transcriptome-wide Association Studies (TWAS). Here we provide QTWAS results on the summary statistics from ten GWAS studies on brain disorders, including five neuropsychiatric traits: schizophrenia (SCZ), attention-deficit/hyperactivity disorder (ADHD), bipolar disorder (BD), autism spectrum disorder (ASD), and major depressive disorder (MDD); and four neurodegenerative traits: Alzheimer’s disease (AD_Kunkle and AD_Jansen), Parkinson’s disease (PD), multiple sclerosis (MS) and amyotrophic lateral sclerosis (ALS).

- **App link:** [tianyingw.shinyapps.io/QTWAS/](https://tianyingw.shinyapps.io/QTWAS/).


## Estimating quantile curves for zero-inflated outcomes
- **Student's name:** Zirui Wang. (This work was finished when Zirui was a junior undergraduate student at Tsinghua University from 2021-2022.)

<img align="center" src="/img/Roseburia_histogram.png" alt="" width="700">

- **Summary:** We consider the complex data modeling problem motivated by the zero-inflated and overdispersed microbiome read count data. Several parametric approaches have been proposed to address issues of zero inflation and overdispersion, such as zero-inflated Poisson regression and zero-inflated Negative Binomial regression. However, parametric assumptions could be easily violated in real-world applications. In this project, we propose a semiparametric single-index quantile regression framework, which is flexible to include a wide range of possible association functions and adaptable to the various zero proportions across subjects. We establish the asymptotic normality of the index coefficients estimator and the asymptotic convergence rate of the nonparametric quantile regression curve estimation. Through Monte Carlo simulation studies and the application in a microbiome study, we demonstrate the superior performance of the proposed method. The above figure shows how our proposed method fits the real microbiome data (Roseburia) better than other methods.

- **Related paper:** <ins>Wang, Z.</ins> and **Wang, T.<b>*</b>** (2022+). _"A Semiparametric Quantile Single-Index  Model for Zero-Inflated and Overdispersed Outcomes"_, under review.




