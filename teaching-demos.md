---
layout: page
title: Teaching Demos
permalink: /teaching-demos/
---

This page collects interactive statistics demos that I have created for teaching, outreach, and self-guided learning.

The goal of these demos is to make statistical ideas easier to see, manipulate, and discuss. Most of them run directly in the browser, with no login required. They are intended as conceptual companions to lectures, activities, problem sets, and formal derivations, rather than as replacements for mathematical arguments.

Many of the demos are designed for guided use with younger learners, including ages 9-14, while still being useful for introductory statistics courses.

## How to use these demos

Each demo is built around one main statistical idea. The demos work best when students first make a prediction, then interact with the simulation, and then discuss what changed and what stayed stable.

The suggested levels below are approximate. Instructors may adapt the demos for different audiences by changing the discussion questions, notation, and amount of mathematical detail.

## Demo catalog

| Demo | Main idea | Recommended level | Format |
|:--|:--|:--|:--|
| [Law of Large Numbers](/demos/lln/) | Repeated sampling, sample averages, long-run stability | Ages 9-14 guided, general audience, introductory statistics | Interactive browser demo |
| [Central Limit Theorem](/demos/clt/) | Sampling distributions, sample averages, normal approximation | Ages 9-14 guided, introductory statistics | Interactive browser demo |
| [Bootstrap Resampling](/demos/bootstrap/) | Resampling with replacement, bootstrap means, standard error | Ages 9-14 guided, introductory statistics | Interactive browser demo |
| [P-values and Errors](/demos/pvalue/) | P-values, alpha, beta, Type I error, Type II error, power | Ages 9-14 guided, introductory statistics | Interactive browser demo |

## Featured demos

### [Law of Large Numbers](/demos-lln/)

This demo illustrates how sample averages stabilize as the sample size increases. Students can run repeated simulations, change the sample size, and observe how the empirical average moves toward the population mean.

**Useful for:** introducing repeated sampling, randomness, simulation, and the distinction between a single random outcome and a long-run pattern.

**Possible classroom prompts:**

- What changes when the sample size increases?
- Does the sample average always move closer to the population mean?
- How is long-run stability different from certainty in any one experiment?
- What does the demo show that a formula alone may not make visually obvious?

### [Central Limit Theorem](/demos-clt/)

This demo shows how averages from repeated samples can become more mound-shaped than the original population. Students can change the sample size and compare the population shape, the distribution of sample averages, and a normal approximation.

**Useful for:** introducing sampling distributions, sample averages, standard error, and why normal approximations appear in many statistical methods.

**Possible classroom prompts:**

- Are we looking at individual observations or sample averages?
- What happens to the distribution of averages when the sample size gets larger?
- Why can the average look more regular than the original population?
- When might the normal approximation still look rough or imperfect?

### [Bootstrap Resampling](/demos-bootstrap/)

This demo explains the bootstrap by treating the observed sample as a resampling bag. Students can see that each bootstrap resample is drawn with replacement and has the same size as the original sample.

**Useful for:** introducing resampling with replacement, bootstrap samples, bootstrap means, and the idea that the bootstrap standard error estimates the sampling variability of an estimator.

**Possible classroom prompts:**

- Why do we put each draw back before drawing again?
- Why should the bootstrap resample have the same size as the original sample?
- What is changing across bootstrap resamples?
- Is the bootstrap standard error describing the spread of raw values or the spread of sample means?

### [P-values and Errors](/demos-pvalue/)

This demo begins with two samples and a one-sided two-sample test, then connects the p-value decision rule to repeated testing. It shows alpha, beta, Type I error, Type II error, correct no alarm, and power using linked shaded regions and simulation bars.

**Useful for:** explaining what a p-value does in one test, and how Type I error, Type II error, and power describe long-run behavior over repeated tests.

**Possible classroom prompts:**

- What would the data look like if the two groups had the same true average?
- What does it mean to reject the null hypothesis?
- Which shaded region is alpha, and why is it a false alarm?
- Why do beta and power add up to 1?
- How is one p-value different from a long-run error rate?

## Topics I plan to add

Future demos may include:

- Confidence interval coverage
- Sampling variability
- Regression leverage and influence
- Bias and variance
- Bayesian updating
- Multiple testing
- Randomization inference

## Notes

These demos are created and maintained by me. They are designed for teaching and conceptual exploration. Unless otherwise noted, the demos use simulated or publicly available examples and do not collect student data.

Some demos may be revised over time as I use them in teaching and receive feedback from students and colleagues.
