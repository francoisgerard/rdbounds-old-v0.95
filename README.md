## Manipulation Robust Regression Discontinuity Bounds Estimation in R - Beta Version (0.95)

This is a public repository for the R package \code{rdbounds}, implementing the estimation procedure developed in [Bounds on Treatment Effects in Regression Discontinuity Designs under Manipulation of the Running Variable, with an Application to Unemployment Insurance in Brazil](http://www.nber.org/papers/w22892, "NBER Working Paper"), by François Gerard, Miikka Rokkanen, and Christoph Rothe. See [rdbounds.pdf](rdbounds.pdf) for details.

This is a **beta** version of the code and is still undergoing testing. We appreciate any feedback or issues noted. Please direct your comments to leonard.goff at columbia.edu.

You may install the ```rdbounds``` package directly from this repository using the ```devtools``` package, as follows:

```{r}
library(devtools)
install_github("leonardgoff/rdbounds")
```

Alternatively, you may download [rdbounds_0.95.tar.gz](rdbounds_0.95.tar.gz) and install the package from source code.

Here's some test code to get you going, once installed:

```{r}
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
