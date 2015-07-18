---
layout: post
title: Matrix Dimension Tricks in R
---

In this post I wanna share some **R** tricks on correctly specifying the dimension of a matrix. Probably most of the data analytics projects in **R** involve playing with a lot of matrices, and carelessness on specifying the dimensions of these matrices might very likely result in the "<font color="red">non-conformable arguments</font>" error. However, generating an error isn't the worst case. At least you can locate the bug and with enough amount of time you should still be able to fix it. In the worst scenario, your algorithm will generate the wrong thing without any error or warning messages. Here is an example:

{% highlight js %}
set.seed(1000)

n <- 5; p <- 3

group <- c(1,1,2,3,3)

X <- matrix(rnorm(n*p),n,p)

tXX <- array(0,c(p,p,3))

for (k in 1:3){

  tXX[,,k] <- t(X[group==k,])%*%X[group==k,]

}
{% endhighlight %}

In the above example, $$\boldsymbol{X}\in\Re^{n\times p}$$ is a design matrix for 5 units with 3 covariates. These 5 units fall into 3 groups and the algorithm tends to calculate $$\boldsymbol{X}^{T}\boldsymbol{X}$$ for each group. At a first glance, you might not be able to find and incorrectness in this piece of code (at least I didn't!). However, if you output  `tXX[,,2]` you will immediatebly realize that there is something wrong. The output is as follows:

{% highlight js %}
          [,1]      [,2]      [,3]

[1,] 0.5344658 0.5344658 0.5344658

[2,] 0.5344658 0.5344658 0.5344658

[3,] 0.5344658 0.5344658 0.5344658
{% endhighlight %}
