---
layout: post
title: Matrix Dimension Tricks in R
---

In this post I wanna share some **R** tricks on correctly specifying the dimension of a matrix. Probably most of the data analytics projects in **R** involve playing with a lot of matrices, and carelessness on specifying the dimensions of these matrices might very likely result in error '<font color="red">non-conformable arguments</font>'. However, generating an error isn't the worst case. At least you can locate the bug and with enough amount of time you should still be able to fix it. In the worst scenario, your algorithm will generate the wrong thing without any error or warning messages. Here is an example:

{% highlight js %}
n <- 5; p <- 3

group <- c(1,1,2,3,3)

X <- matrix(rnorm(n*p),n,p)

tXX <- array(0,c(p,p,3))

for (k in 1:3){

  tXX[,,k] <- t(X[group==k,])%*%X[group==k,]

}
{% endhighlight %}
