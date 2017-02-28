## Manipulation Robust Regression Discontinuity Bounds Estimation in R - Beta Version (0.95)

This is a public repository for the R package ```rdbounds```, implementing the estimation procedure developed in [Bounds on Treatment Effects in Regression Discontinuity Designs under Manipulation of the Running Variable, with an Application to Unemployment Insurance in Brazil](http://www.nber.org/papers/w22892, "NBER Working Paper"), by François Gerard, Miikka Rokkanen, and Christoph Rothe.

This is a **beta** version of the code and is still undergoing testing. We appreciate any feedback or issues noted. Please direct your comments to leonard.goff at columbia.edu.

See [rdbounds.pdf](rdbounds.pdf) for documentation. The code is viewable in [R/rdbounds.R](https://github.com/francoisgerard/rdbounds/blob/master/R/rdbounds.R).

You may install the ```rdbounds``` package directly from this repository using the ```devtools``` package, by running the following commands in R (the first two lines may not be necessary if you already have the packages ```formattable``` and ```data.table``` installed):

```{r}
install.packages("formattable")
install.packages("data.table")
install.packages("devtools")
library(devtools)
install_github("francoisgerard/rdbounds")
```

Alternatively, you may download [rdbounds_0.95.tar.gz](rdbounds_0.95.tar.gz) and install the package from source code. You will need to also install the packages ```formattable``` and ```data.table``` if you do not have them already.

Here's some test code to get you going, once installed:

```{r}
library(formattable)
library(data.table)
library(rdbounds)
df<-rdbounds_sampledata(30000, covs=TRUE)
rdbounds_est<-rdbounds(y=df$y,x=df$x, covs=df$cov, treatment=df$treatment, c=0,
                       discrete_x=FALSE, discrete_y=FALSE, bwsx=c(.1,1), bwy = .1,
                       kernel="triangular", orders=c(1,1),
                       evaluation_ys = seq(from = 0, to=23, by=.1), ymin=0, ymax=23,
                       right_effects=TRUE, yextremes = c(0,23),
                       num_bootstraps=c(1,1))
rdbounds_summary(rdbounds_est, title_prefix="Sample Data Results")
```
