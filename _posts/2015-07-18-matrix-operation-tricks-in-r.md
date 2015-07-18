---
layout: post
title: Matrix Operation Tricks in R
---

I wanna share some **R** tricks on matrix operations. Carelessness in matrix manipulation might very likely result in the "<font color="red">non-conformable arguments</font>" error. However, you are still very lucky if your **R** program is terminated and generates an error message, meaning that you can locate the bug and fix it. I will share with you some **R "trapps"**. These **"trapps"** might remain invisible even to the experienced **R** users. Worse is, they will not generate any errors hence are extremely hard to be targeted during debugging. I have encountered such **"trapps"** several times and it took me forever long to figure out what is wrong. I hope the tricks I am sharing with you can help avoid such **"trapps"**. But before that, let's first understand these **"trapps"** by the following simple example.

### Can you find the trap?

In this example, $$\boldsymbol{X}\in\Re^{n\times p}$$ is a design matrix for 5 units with 3 covariates. These 5 units fall into 3 groups. The algorithm tends to calculate $$\boldsymbol{X}^{T}\boldsymbol{X}$$ for each group.

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

At a first glance, you might not be able to find any incorrectness in this piece of code (at least I didn't!). However, you will immediately realize that there is something wrong after seeing the following output:

{% highlight js linenos %}
> tXX[,,2]

          [,1]      [,2]      [,3]

[1,] 0.5344658 0.5344658 0.5344658

[2,] 0.5344658 0.5344658 0.5344658

[3,] 0.5344658 0.5344658 0.5344658
{% endhighlight %}

### Here is what is wrong

Here are several other outputs from the code:

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

Now you may have noticed what are wrong. This example illustrates three "trapps" in **R**:

* By default, **R** will drop a dimension of a matrix/array when you select only one row/column/subarray from that dimension;

* `t(v)` will return a 1-by-p matrix where v is a p-dimensional vector in **R**;

* In `a%*%b`, if a or b is a p-dimensional vector, it will be automatically treated as a p-by-1 matrix. If the dimension of this matrix multiplication is non-conformable (e.g., 1-by-p multiplied by 1-by-p), the **R** operator will return the inner product (a scalar) of a and b;

* A is a 3-dimensional array and a is a scalar, `A[,,1] <- a` will not generate an error message in **R**, instead, each entry of `A[,,1]` will be changed to a.

### Tricks that might be helpful

The main idea of the following two tricks is to ensure that any matrices in matrix operatioins will not be coerced into **R** vectors.

#### 1. Use "drop = FALSE" when selecting subarrays

**R** uses `drop = TRUE` as its default. The trick is, whenever the selected subarray participates in matrix operations, explicitly setting `drop = FALSE`. An example can be found below:

{% highlight js linenos %}
> X[1,]
[1] -0.4457783 -0.3854893 -0.9824278
> X[1,,drop=FALSE]
           [,1]       [,2]       [,3]
[1,] -0.4457783 -0.3854893 -0.9824278
{% endhighlight %}

#### 2. Use "as.matrix" to create vectors

Whenever a vector is going to participates in matrix operations, specify it as a column vector in **R** using `as.matrix()`. An example can be found below:

{% highlight js linenos %}
> 1:3

[1] 1 2 3

> as.matrix(1:3)

     [,1]

[1,]    1

[2,]    2

[3,]    3
{% endhighlight %}

------

So I haved described several **R "trapps"** that have given me a really hard time before and my own tricks to avoid them. hopefully this post will help.

### Cheers!
