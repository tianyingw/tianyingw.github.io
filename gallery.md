---
layout: page
title: Showcase
---

Welcome to the gallery of research projects with undergraduate students I supervised at Tsinghua University. Here are three examples. More on the way!

## Modeling zero-inflated data with error-in-variables
- **Student's name:** Roulan Jiang. (This work was conducted when Roulan was a senior undergraduate student at Tsinghua University from 2021-2022.)
- **Related paper:** <ins>Jiang, R.</ins>, Zhan, X.*, and **Wang, T.<b>*</b>** (2022+) ["A Flexible Zero-Inflated Poisson-Gamma Model with Application to Microbiome Read Count Data"](https://arxiv.org/pdf/2207.07796.pdf), under review.

<img align="right" src="/img/Romero_32_violin_pre_Race01.jpg" alt="" width="400">

- **Summary:** In microbiome studies, it is of interest to use a sample from a population of microbes, such as the gut microbiota community, to estimate the population proportion of these taxa. However, due to biases introduced in sampling and preprocessing steps, these observed taxa abundances may not reflect true taxa abundance patterns in the ecosystem. Repeated measures including longitudinal study designs may be potential solutions to mitigate the discrepancy between observed abundances and true underlying abundances. Yet, widely observed zero-inflation and over-dispersion issues can distort downstream statistical analyses aiming to associate taxa abundances with covariates of
interest. We propose a Zero-Inflated Poisson Gamma (ZIPG) framework to address the aforementioned challenges. From a perspective of measurement errors, we accommodate the discrepancy between observations and truths by decomposing the mean parameter in Poisson regression into a true abundance level and a multiplicative measurement of sampling variability from the microbial ecosystem. Then, we provide flexible modeling by
connecting both mean abundance and the variability to different covariates, and build valid statistical inference procedures for both parameter estimation and hypothesis testing. Through comprehensive simulation studies and real data applications, the proposed ZIPG method provides significant insights into distinguished differential variability and abundance.



## Quantile TWAS Genome Browser (Shiny app)
- **Student's name:** Weijing Yin. (This work was conducted as a summer project in 2022 when Weijing was a sophomore undergraduate student at Tsinghua University.)
- **Summary:** This visualization is based on QTWAS, a quantile regression model for Transcriptome-wide Association Studies (TWAS). Here we provide QTWAS results on the summary statistics from ten GWAS studies on brain disorders, including five neuropsychiatric traits: schizophrenia (SCZ), attention-deficit/hyperactivity disorder (ADHD), bipolar disorder (BD), autism spectrum disorder (ASD), and major depressive disorder (MDD); and four neurodegenerative traits: Alzheimer’s disease (AD_Kunkle and AD_Jansen), Parkinson’s disease (PD), multiple sclerosis (MS) and amyotrophic lateral sclerosis (ALS). 
- **App link:** [tianyingw.shinyapps.io/QTWAS/](https://tianyingw.shinyapps.io/QTWAS/).


## Inference on single-index zero-inflated quantile regression models
- **Student's name:** Zirui Wang. (This work is still ongoing. Zirui is a senior undergraduate student at Tsinghua University.)
- **Summary:** Single index models provide flexible data analysis than linear model while remaining interpretability. Though single-index model has been studied under the quantile regression framework, it cannot be applied directly to zero-inflated outcomes, which are commonly observed in single-cell data, microbiome data, counts data, etc. In this paper, we propose a single-index quantile regression model for zero-inflated outcomes. We establish the asymptotic normality of the index coefficients estimator as well as the entire quantile regression curve. Through extensive numerical studies and applications with UK Biobank data, we illustrate the performance of our approach and validate our asymptotic results.
- **Related paper:** will be posted on arXiv soon.
