---
layout: post
title:  "Data Science"
description: "Notes for Data Science. Extract valuable insights and optimize performance through analytics techniques."
date:   2023-05-16 12:11:31 +0100
categories: [Notes,Data Science]
tags: [Data Science]
math: true
---

## The Process
![The Process Steps Mind Map](/Notes_for_Data_Science/Data%20Science%20The%20Process.png)

*The Process Steps Mind Map Created by A.Prophett*

## Uncertainty in the data
![Uncertainty in the data Mind Map](Notes_for_Data_Science/Uncertainty%20in%20the%20data.png)
*Uncertainty in the data Mind Map Created by A.Prophett*


## Flash Cards
<iframe src="https://quizlet.com/803477515/flashcards/embed?i=1oro1z&x=1jj1" height="500" width="100%" style="border:0"></iframe>

## Formulas
SD

$$
\sigma = \sqrt{\frac{\sum(X-\mu)^2}{N}}
$$

SEM

$$
SEM=\frac{SD}{\sqrt{n}}
$$

Bayes Rule

$$
P(HYP|DATA)=\frac{P(DATA|HYP)P(HYP)}{P(DATA)}
$$

- `P(HYP|DATA)` **posterior**
- `P(DATA)` **Normalising Factor**
- `P(HYP)` **Prior**
- `P(DATA|HYP)` **Likelihood**

P(Data) with a discrete set of hypotheses

$$
P(Data)=P(data|HYP_1)+P(data|HYP_2)+...P(data|HYP_N)\\=\sum_{i=0}^{hyp \space count}P(data|HYP_i)
$$

C**ombining variables**

Adding Variances (IFF X and Y are independent)

$$
\sigma_z=\sqrt{\sigma_x^2+\sigma_y^2}
$$

Adding means

$$
\mu_z=\mu_x+\mu_y
$$


> This post has not been verified and may contain false information and opinions. Any corrections and improvements are welcome. Please see [About](/about) for details.
{: .prompt-warning }