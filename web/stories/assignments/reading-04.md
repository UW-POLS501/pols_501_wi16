# Reading Assignment 4

Complete all the even numbered exercises in *OpenIntro Statistics* Chapter 4.


Submit as a Word Document or PDF via Canvas. Answers must be typed.

This requires calculating cumulative probabilities and quantiles of the normal distributions. To calculate these in R, you can use the functions `pnorm` and `qnorm`.

For solving questions, even though you are calculating these tests manually, 
save yourself some work by doing the calculations in R rather than by hand and calculator.

For example:

**Ex 4.15** The confidence interval is $3.2 \pm 0.3 = (2.9, 3.5)$ relationships.
The confidence interval for a sample mean is,
$$
\bar{x} \pm z^*_{\alpha/2} \frac{s}{\sqrt{n}} .
$$
The values of the sample size $n$, sample mean $\bar{x}$, and sample standard deviation $s$ given in the problem:

```r
n <- 203
xbar <- 3.2
s <- 1.97
```
The standard error, $SE = s / \sqrt{n}$,

```r
se <- s / sqrt(n)
se
```

```
## [1] 0.1382669
```
The critical value, $z^*$, for a 95% CI is 1.96, but we can calculate it directly using `qnorm()`.
Since qnorm will calculate the quantile for an area on the lower tail, it will be negative, so we need to switch the sign to ensure it is positive in our calculations.

```r
# 
alpha <- 0.05
z_star <- -qnorm(0.05 / 2)
z_star
```

```
## [1] 1.959964
```
Margin of error, $ME = z^* \times SE$

```r
me <- z_star * se
me
```

```
## [1] 0.2709981
```
The confidence interval, $\bar{x} \pm ME$,

```r
xbar + c(-1, 1) * me
```

```
## [1] 2.929002 3.470998
```
This assumes the criteria for inference are met; these would need to be checked.

**Ex 4.25**
We can reject the null hypothesis that the average waiting time of ER patients is the same as last year's average of 127 minutes, and accept the alternative hypothesis that it is different.
The P-value of a two-sided hypothesis test of the sample mean was $.031 < .05$.

The null (alternative) hypothesis for this test is that the average waiting time of ER patients
is the same as (different than) last year's average of 127 minutes.
Formally, the hypotheses are
$$
\begin{aligned}[t]
H_0: & \mu = 127 \\
H_a: & \mu \neq 127
\end{aligned}
$$
The test statistic for a hypothesis test of the mean is,
$$
Z = \frac{\bar{x} - \mu_0}{s / \sqrt{n}}
$$
where $Z$ is distributed standard normal.

The values of the sample size $n$, sample mean $\bar{x}$, sample standard deviation $s$, and null hypothesis value of the population mean $\mu_0$ given in the problem:

```r
n <- 64
x_bar <- 137.5
s <- 39
mu_0 <- 127
```
The standard error of the sample mean, $SE = s / sqrt{n}$,

```r
se <- s / sqrt(n)
se
```

```
## [1] 4.875
```
The test-statistic, $Z = (\bar{x} - \mu_0) / SE$,

```r
z <- (x_bar - mu_0) / se
z
```

```
## [1] 2.153846
```
Find the two-sided tail area with the normal distribution,

```r
2 * pnorm(-abs(z))
```

```
## [1] 0.03125224
```
When calculating the P-value for a two-sided test with `pnorm`, `-abs()` is used to ensure that the area being calculated is the lower tail, and this area is multiplied by two to get the area of both tails.
This assumes the criteria for inference are met; these would need to be checked.

