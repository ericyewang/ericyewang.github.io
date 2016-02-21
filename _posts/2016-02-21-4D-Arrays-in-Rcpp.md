# Store 4D arrays in Rcpp
Ye (Eric) Wang  
February 21, 2016  

In this blog I will present a method to pass a 4-dimensional array in R to Rcpp functions for efficiently matrix operations over the 2-dimensional slices of this array. The method can be generalized to higher dimensional arrays. I will assume the readers have some familiarity with Rcpp and Armadillo. For more details on Rcpp see <http://www.rcpp.org>. For more details on Armadillo see  <http://arma.sourceforge.net/docs.html#operators>.

As we all know, matrix operatinos can be done efficiently by calling Armadillo inside Rcpp. Armadillo does provide an object called "cube" to deal with 3D arrays. However, its abillity of dealing with arrays with dimension higher than three is quite limited.

4D arrays are pretty common in many statistical applications, for instance, in a hierarchical clustering modeling application with two group indices, covariance matrices (d by d) of each subpopulation i (i = 1,...,n) for each cluster j (j = 1,...,m) can be stored into a 4D array (d by d by n by m). In this example, one would also like to apply matrix operations efficiently on the d by d matrix slices (the covariance matrices) of the array. The story can be easily generalized to higher dimensional arrays. This motivates me to find an general and efficient way to achieve this goal in Rcpp, and below is my best attempt using the vector library of c++:


```r
suppressMessages( require(Rcpp) )
suppressMessages( require(inline) )

code <- '  Rcpp::List xlist(x); 
           int n = xlist.size();
           int mm = Rcpp::as<int>(m);
           std::vector<arma::mat> vcube(n*mm);

           // Store the memory locations of the 3d cubes
           for(int i = 0; i < n; i++) {
              Rcpp::NumericVector nvxlist(xlist[i]);
              IntegerVector arrayDims = nvxlist.attr("dim");
              arma::cube cubeM(nvxlist.begin(), arrayDims[0], arrayDims[1], arrayDims[2]);
              for(int j = 0; j < mm; j++){
                 vcube[i*mm+j] = cubeM.slice(j);
              }
            }

            return(Rcpp::wrap(vcube[0]*vcube[1]));'

fx <- cxxfunction(signature(x='List',m='numeric'), plugin='RcppArmadillo', body = code)
```

The idea is pretty simple, you need to re-index your array into a long vector of arma::mat objects. In the above case, the matrix slice x[,,i,j] has been stored into the std::vector object vcube[i*m+j]. Below is a little test, just to show that the function is doing its job.


```r
set.seed(4321)
x <- list(array(rnorm(8),c(2,2,2)), 
          array(rnorm(8),c(2,2,2)), 
          array(rnorm(8),c(2,2,2)))
fx(x,2)
```

```
##          [,1]      [,2]
## [1,] 1.209656 0.2674727
## [2,] 1.382880 0.2313774
```

```r
x[[1]][,,1]%*% x[[1]][,,2]
```

```
##          [,1]      [,2]
## [1,] 1.209656 0.2674727
## [2,] 1.382880 0.2313774
```

When you want to pass a higher dimensional array to Rcpp, you can follow exactly the same strategy.
