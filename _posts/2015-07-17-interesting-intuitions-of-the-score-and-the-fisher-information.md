---
layout: post
title: Interesting intuitions of the score and the Fisher information
---

In this post I'm going to present two interesting intuitions about the **score function** and the **Fisher information**. Prior to that let's have a quick review of these two concepts:

> **Score function**: the gradient of the log-likelihood function. To be specific, let's assume that the likelihood of the observation \\(\boldsymbol{X}\\) is \\(L(\theta;\boldsymbol{X})\\), then the score function \\(S(\theta;\boldsymbol{X})\\) is defined as \\(S(\theta; \boldsymbol{X})=\frac{\partial}{\partial\theta} \log L(\theta; \boldsymbol{X})\\). Intuitively, the score function measures how sensitive is the log-likelihood to the choice of parameters.

> **Fisher information**: the variance of the score function. To be specific, let's assume again that the score function of the observation \\(\boldsymbol{X}\\) is \\(S(\theta;\boldsymbol{X})\\), then the fisher information is defined as $$E_{\boldsymbol{X}}\bigg(S(\theta;\boldsymbol{X})^2\bigg)$$. If the log-likelihood is twice differentiable with respect to \\(\theta\\), then the Fisher information is equivalent to $$-E_{\boldsymbol{X}}\bigg(\frac{\partial}{\partial\theta}S(\theta;\boldsymbol{X})\bigg)$$ or $$-E_{\boldsymbol{X}}\bigg(\frac{\partial^{2}}{\partial\theta^{2}}\log L(\theta; \boldsymbol{X})\bigg)$$. Hence the Fisher information is also the expected curvature of the log-likelihood function.

-----

For a more detailed review, you can visit the [Wikipedia page](https://en.wikipedia.org/wiki/Fisher_information). In this post however, I will just give you two of my personal intuitions that might be interesting and help you understand these two fundamental concepts.

### Why is the expectation of the score function zero?

You can mathematically prove that the expectation $$E_{\boldsymbol{X}}\bigg(S(\theta;\boldsymbol{X})\bigg)$$ equals 0 under some very mild conditions, the prrof can be found [here](https://en.wikipedia.org/wiki/Score_(statistics)#Mean).

### Browser support

Poole and its themes are by preference a forward-thinking project. In addition to the latest versions of Chrome, Safari (mobile and desktop), and Firefox, it is only compatible with Internet Explorer 9 and above.

### Download

Poole is developed on and hosted with GitHub. Head to the <a href="https://github.com/poole/poole">GitHub repository</a> for downloads, bug reports, and features requests.

Thanks!
