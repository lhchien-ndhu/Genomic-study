two sample t test with summary stat.
================
Li-Hsin Chien
2026-02-26

$$X \sim N(\mu_x,\sigma_x^2), ~~~~ Y \sim N(\mu_y,\sigma_y^2)$$

Data: $$(x_1,...,x_n), (y_1,...,y_m) $$

Summary statistics: $$\bar{x}=\frac{1}{n} \sum_{i=1}^n x_i$$,
$$\bar{y}=\frac{1}{m} \sum_{i=1}^m y_i$$,
$$s_x^2=\frac{1}{n-1}\sum_{i=1}^n (x_i-\bar{x})^2$$,
$$s_y^2=\frac{1}{m-1}\sum_{i=1}^m (y_i-\bar{y})^2$$

Hypothesis testing:

$$H_0: \mu_x = \mu_y; ~~~ H_1: \mu_x \neq \mu_y$$

Assume $\sigma_x^2=\sigma_y^2$, the test statistics:

$$ t=\frac{\bar{x}-\bar{y}}{S_p\sqrt{\frac{1}{n}+\frac{1}{m}}}, $$
$$ S_p^2 = \frac{(n-1)s_x^2+(m-1)s_y^2}{n+m-2}$$

$$ t  \sim \text{ t-dist. with } df= n+m-2 $$

``` r
x.bar=50
y.bar=52

sd.x = 13
sd.y = 12

n.x=5000
n.y=5000

sp <- sqrt(((n.x-1)*sd.x^2+(n.y-1)*sd.y^2)/(n.x+n.y-2))

t <- (x.bar-y.bar)/(sp*sqrt(1/n.x+1/n.y))

df <- n.x+n.y-2

(p.value <- 2*pt(-abs(t), df=df))
```

    ## [1] 1.455289e-15

``` r
#install.packages("BSDA")
library(BSDA)

?tsum.test

r<-tsum.test(x.bar,sd.x,n.x,y.bar,sd.y,n.y,var.equal=TRUE)
r$p.value
```

    ## [1] 1.455289e-15
