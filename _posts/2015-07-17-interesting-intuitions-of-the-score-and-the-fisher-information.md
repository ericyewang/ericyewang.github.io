---
layout: post
title: Interesting intuitions of the score and the Fisher information
---

In this post I'm going to present two interesting intuitions about the **score function** and the **Fisher information**. Prior to that let's have a quick review of these two concepts:

> **Score function**: the gradient of the log-likelihood function. To be specific, let's assume that the likelihood of \(\bm{X}\) is \(L(\theta;\bm{X})\), then the score function \(S(\theta;\bm{X})\) is defined as

$$S(\theta;\bm{X})=\frac{\partial}{\partial\theta \log L(\theta;\bm{X})}$$

-----

Poole is the butler for [Jekyll](http://jekyllrb.com), the static site generator. It's designed and developed by [@mdo](https://twitter.com/mdo) to provide a clear and concise foundational setup for any Jekyll site. It does so by furnishing a full vanilla Jekyll install with example templates, pages, posts, and styles.

There are currently two themes built on Poole:

* [Hyde](http://hyde.getpoole.com)
* [Lanyon](http://lanyon.getpoole.com)

Learn more and contribute on [GitHub](https://github.com/poole).

###### What's included

Poole is a streamlined Jekyll site designed and built as a foundation for building more meaningful themes. Poole, and every theme built on it, includes the following:

* Complete Jekyll setup included (layouts, config, [404]({{ site.baseurl }}/404.html), [RSS feed]({{ site.baseurl }}/atom.xml), posts, and [example page]({{ site.baseurl }}/about))
* Mobile friendly design and development
* Easily scalable text and component sizing with `rem` units in the CSS
* Support for a wide gamut of HTML elements
* Related posts (time-based, because Jekyll) below each post
* Syntax highlighting, courtesy Pygments (the Python-based code snippet highlighter)

Additional features are available in individual themes.

### Browser support

Poole and its themes are by preference a forward-thinking project. In addition to the latest versions of Chrome, Safari (mobile and desktop), and Firefox, it is only compatible with Internet Explorer 9 and above.

### Download

Poole is developed on and hosted with GitHub. Head to the <a href="https://github.com/poole/poole">GitHub repository</a> for downloads, bug reports, and features requests.

Thanks!
