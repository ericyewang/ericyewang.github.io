---
layout: post
title: Matrix Dimension Tricks in R
---

In this post I wanna share some **R** tricks on correctly specifying the dimension of a matrix. Probably most of the data analytics projects in **R** involve playing with a lot of matrices, and carelessness on specifying the dimensions of these matrices might very likely result in the "<font color="red">non-conformable arguments</font>" error. However, generating an error isn't the worst case. At least you can locate the bug and with enough amount of time you should still be able to fix it. In the worst scenario, your algorithm will generate the wrong thing without any error or warning messages. Let's start with the following example

#### Can you tell what is wrong?

{% highlight js linenos %}
set.seed(1000)

n <- 5; p <- 3

group <- c(1,1,2,3,3)

X <- matrix(rnorm(n*p),n,p)

tXX <- array(0,c(p,p,3))

for (k in 1:3){

  tXX[,,k] <- t(X[group==k,])%*%X[group==k,]

}
{% endhighlight %}

In the above example, $$\boldsymbol{X}\in\Re^{n\times p}$$ is a design matrix for 5 units with 3 covariates. These 5 units fall into 3 groups and the algorithm tends to calculate $$\boldsymbol{X}^{T}\boldsymbol{X}$$ for each group. At a first glance, you might not be able to find and incorrectness in this piece of code (at least I didn't!). However, you will immediately realize that there is something wrong after seeing the following output:

{% highlight js linenos %}
> tXX[,,2]

          [,1]      [,2]      [,3]

[1,] 0.5344658 0.5344658 0.5344658

[2,] 0.5344658 0.5344658 0.5344658

[3,] 0.5344658 0.5344658 0.5344658
{% endhighlight %}

##### Here is what is wrong

Before answering what is wrong, let me give you several other outputs from the code:

{% highlight js linenos %}
> X[group==2,]

[1] 0.04112631 0.71975069 0.12138119

> t(X[group==2,])

           [,1]      [,2]      [,3]

[1,] 0.04112631 0.7197507 0.1213812

> t(X[group==2,])%*%X[group==2,]

          [,1]

[1,] 0.5344658
{% endhighlight %}

Now you may have noticed that `X[group==2,]` returns a vector instead of a 1-by-3 matrix. This is because

> By default, **R** will drop a dimension of a matrix when you select only one row/column from that dimension. 

And the matrix transpose function `t()` simply returns a 1-by-3 matrix instead of the desired 3-by-1 matrix. Then it seems that the matrix multiplication operator `%*%` will return the inner product (scaler) of two 1-dimensional object whenever their dimensions are non-conformable. In the end, as you have seen, the scaler was applied to all entries of the 3-by-3 matrix `tXX[,,2]`.
