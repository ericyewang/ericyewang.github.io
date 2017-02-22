---
layout: post
title: Matrix Operation Tricks in R
---

As we all know, careless matrix manipulation in **R** will very likely result in the "<font color="red">non-conformable arguments</font>" error. The good news is, your **R** program will terminate itself and generates an error message, helping you locate the bug and fix it.

When you are not lucky enough you might fall into some what I call **R "trapps"**, without even knowing it! These **"trapps"** is neglected even by the experienced **R** users. Worse is, they will not generate any errors hence are extremely hard to be targeted during debugging.

I have met with such **"trapps"** several times and it took me forever long to figure out what is wrong. To battle them I have developed some tricks by myself and I am sharing them with you. I hope they can help you avoid such **"trapps"**. But before that, let's first see some of these **"trapps"** in the following simple example.

------

### Can you find the trap?

In this example, $$\boldsymbol{X}\in\Re^{n\times p}$$ is a design matrix for 5 units with 3 covariates. These 5 units fall into 3 groups. The algorithm tends to calculate $$\boldsymbol{X}^{T}\boldsymbol{X}\in\Re^{p\times p}$$ for each group.

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

At a first glance, you might not be able to find any incorrectness in this piece of code (at least I didn't!). **R** is also super happy with it and no error will be generated! You might just happily report the outputs and start watching Youtube. However, if you are careful enough you will realize that there is something wrong after examining the output:

{% highlight js linenos %}
> tXX[,,2]

          [,1]      [,2]      [,3]

[1,] 0.5344658 0.5344658 0.5344658

[2,] 0.5344658 0.5344658 0.5344658

[3,] 0.5344658 0.5344658 0.5344658
{% endhighlight %}

### Here is what is wrong

Let's first look at some more details:

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

Now you may have noticed what is going wrong. This example illustrates four "trapps" in **R**:

* By default, **R** will drop a dimension of a matrix/array when you select only one row/column/subarray from that dimension;

* `t(v)` will return a 1-by-p matrix where v is a p-dimensional vector in **R**;

* In `a%*%b`, if a or b is a p-dimensional vector, it will be automatically treated as a p-by-1 matrix. If the dimensions of a and b are non-conformable (e.g., 1-by-p multiplied by 1-by-p), the **R** operator will return the inner product (a scalar) of a and b;

* A is a 3-dimensional array and a is a scalar, running `A[,,1] <- a` will not get an error message in **R**. Instead, each entry of `A[,,1]` will be given value a.

### Tricks that might be helpful

The main idea of the following two tricks is to ensure that any matrices in matrix operatioins will not be coerced into **R** vectors.

#### 1. Use "drop = FALSE" when selecting vectors

**R** uses `drop = TRUE` as its default. This trick is explicitly setting `drop = FALSE`, whenever the selected vectors participates in matrix operations. An example can be found below:

{% highlight js linenos %}
> X[1,]
[1] -0.4457783 -0.3854893 -0.9824278
> X[1,,drop=FALSE]
           [,1]       [,2]       [,3]
[1,] -0.4457783 -0.3854893 -0.9824278
{% endhighlight %}

#### 2. Use "as.matrix" to create vectors

Whenever a vector is going to participate in matrix operations, specify it as a column vector in **R** using `as.matrix()`. An example can be found below:

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

So I haved described several **R "trapps"** that have given me a really hard time. I have shared my own tricks to helped me avoid these **"trapps"**. Note that these **trapps** can only be avoided, but cannot be addressed. I hope that they can help you as well!

### Cheers!
