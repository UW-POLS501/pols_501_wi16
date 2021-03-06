# Reading Assignment 5

Complete all the even numbered exercises in *OpenIntro Statistics* Chapter 5.

Submit as a Word Document or PDF via Canvas. Answers must be typed.

This requires calculating cumulative probabilities and quantiles of the normal distributions. To calculate these in R, you can use the functions `pt` and `qt`.
For solving questions, even though you are calculating these tests manually,
save yourself some work by doing the calculations in R rather than by hand and calculator.

**Ex 5.1** The critical t values are:
$n = 6$, $CL = 90%$,

```r
-qt((1 - .9) / 2, df = 6 - 1)
```

```
## [1] 2.015048
```
$n= 21$, $CL = 98%$,

```r
-qt((1 - .98) / 2, df = 21 - 1)
```

```
## [1] 2.527977
```
$n= 29$, $CL = 95%$,

```r
-qt((1 - .95) / 2, df = 29 - 1)
```

```
## [1] 2.048407
```
$n= 12$, $CL = 99%$,

```r
-qt((1 - .99) / 2, df = 12 - 1)
```

```
## [1] 3.105807
```

**Ex 5.3** The p-values are
$H_a: \mu > \mu_0$, $n = 11$, $T = 1.91$,

```r
pt(1.91, df = 11 - 1, lower.tail = FALSE)
```

```
## [1] 0.04260244
```
$H_a: \mu < \mu_0$, $n = 17$, $T = -3.45$

```r
pt(-3.45, df = 17 - 1)
```

```
## [1] 0.001646786
```
$H_a: \mu \neq \mu_0$, $n = 7$, $T = 0.83$

```r
2 * pt(0.83, df = 7 - 1)
```

```
## [1] 1.561692
```
$H_a: \mu > \mu_0$, $n = 28$, $T = 2.13$

```r
pt(2.13, df = 28 - 1, lower.tail = FALSE)
```

```
## [1] 0.02121769
```

**Ex 5.7**
We can reject the null hypothesis that on average New Yorkers sleep 8 hours a night, and accept the alternative hypothesis that on average they sleep less than 8 hours a night.
The P-value of a two-sided hypothesis test of the sample mean was $.046 < 0.05$.

The null (alternative) hypothesis for this test is that on average New Yorkers sleep (less than) 8 hours a night.
Formally, the hypotheses are
$$
\begin{aligned}[t]
H_0: & \mu = 8 \\
H_a: & \mu < 8
\end{aligned}
$$
The test statistic for a hypothesis test of the mean is,
$$
Z = \frac{\bar{x} - \mu_0}{s / \sqrt{n}}
$$
where $Z$ is distributed standard normal.

The values of the sample size $n$, sample mean $\bar{x}$, sample standard deviation $s$, and null hypothesis value of the population mean $\mu_0$ given in the problem:

```r
n <- 25
x_bar <- 7.73
s <- 0.77
mu_0 <- 8
```
The standard error of the sample mean, $SE = s / sqrt{n}$,

```r
se <- s / sqrt(n)
se
```

```
## [1] 0.154
```
The test-statistic, $T = (\bar{x} - \mu_0) / SE$,

```r
t_stat <- (x_bar - mu_0) / se
t_stat
```

```
## [1] -1.753247
```
Find the one-sided tail area of the Student's t distribution with $n - 1$ degrees of freedom,

```r
pt(t_stat, df = n - 1)
```

```
## [1] 0.04616261
```
Although part (d) can be solved without explicitly calculating a 90% confidence interval, the 90% confidence interval is $7.73 \pm 0.26 = (7.47, 7.99)$,

```r
t_star <- -qt((1 - .9) / 2, df = n - 1)
me <- se * t_star
me
```

```
## [1] 0.2634758
```

```r
x_bar + c(-1, 1) * me
```

```
## [1] 7.466524 7.993476
```


**Ex 5.29**
The test rejects the null hypothesis that the average number of traffic related emergency room admissions are different between Friday the 6th and Friday the 13th.

The test rejects the null (alternative) hypothesis that the average number of traffic related emergency room admissions are the same on (different on) Friday the 6th and Friday the 13th.
Formally, the hypotheses are
$$
\begin{aligned}[t]
H_0: & \mu_{diff} = 0 \\
H_a: & \mu_{diff} \neq 0
\end{aligned}
$$
The test statistic for a hypothesis test for paired difference in means is,
$$
Z = \frac{\bar{x}_{diff} - \mu_0}{s / \sqrt{n}}
$$
where $Z$ is distributed standard normal.

The values of the sample size $n$, sample mean $\bar{x}$, sample standard deviation $s$, and null hypothesis value of the population mean $\mu_0$ given in the problem:

```r
n <- 6
x_bar <- -3.13
s_ <- 3.01
mu__0 <- 0
```
The standard error of the sample mean, $SE = s / sqrt{n}$,

```r
se <- s / sqrt(n)
se
```

```
## [1] 0.3143512
```
The test-statistic, $T = (\bar{x} - \mu_0) / SE$,

```r
t_stat <- (x_bar - mu_0) / se
t_stat
```

```
## [1] -35.40626
```
Find the one-sided tail area of the Student's t distribution with $n - 1$ degrees of freedom,

```r
pt(t_stat, df = n - 1)
```

```
## [1] 1.691098e-07
```

**Ex 3.31**

The null (alternative) hypothesis is that the average weight of chickens that were fed linseed and horsebean are the same (different).
Let $\mu_2$ be the average weight of chickens fed linseed, and $\mu_1$ be the average weight of chickens fed horsebean. Formally, the hypotheses are
$$
\begin{aligned}[t]
H_0: & \mu_{2} - \mu_{1} = 0 \\
H_a: & \mu_{2} - \mu_1 \neq 0
\end{aligned}
$$
The test statistic for a hypothesis test for paired difference in means is,
$$
T = \frac{\bar{x}_2 - \bar{x}_1 - \mu_0}{\sqrt{\frac{s_1^2}{n_1}} + \frac{s_2^2}{n_2}}
$$
where $T$ is distributed Student's t with approximately $\min(n_1, n_2) - 1$ degrees of freedom.

The values of the sample sizes $n$, sample means $\bar{x}$, sample standard deviations $s$, and null hypothesis value of the difference in means $\mu_0$ given in the problem:

```r
mu_0 <- 0
```
The values for linseed fed chickens,

```r
n_2 <- 12
x_bar_2 <- 218.75
s_2 <- 52.24
```
The values for horsebean fed chickens,

```r
n_1 <- 10
x_bar_1 <- 160.20
s_1 <- 38.63
```
The difference in sample means, $\bar{x}_diff = x_2 - x_1$,

```r
x_bar_diff <- x_bar_2 - x_bar_1
x_bar_diff
```

```
## [1] 58.55
```
The standard error of the difference in sample means sample mean, $SE_{diff} = \sqrt{s_2^2 / n_2 + s_1^2 / n_1}$,

```r
se <- sqrt(s_1 ^ 2 / n_1 + s_2 ^ 2 / n_2)
se
```

```
## [1] 19.40737
```
The test-statistic, $T = (\bar{x}_{diff} - \mu_0) / SE_{diff}$,

```r
t_stat <- (x_bar_diff - mu_0) / se
t_stat
```

```
## [1] 3.016896
```
Find the one-sided tail area of the Student's t distribution with $n - 1$ degrees of freedom,

```r
2 * pt(-abs(t_stat), df = min(n_2, n_1) - 1)
```

```
## [1] 0.01455232
```
The test rejects the null hypothesis that the average weights are the same and accepts the alternative hypothesis that they are different (p-value = $0.015 < 0.05$).

The question does not ask to calculate the confidence interval, but the 95% confidence interval for the difference in weights is calculated as follows.
The critical t-value for $df = \min(n_1, n_2) - 1$ is

```r
t_star <- -qt((1 - 0.95) / 2, df = min(n_1, n_2) - 1)
t_star
```

```
## [1] 2.262157
```
The margin of error is $ME_{diff} = t^* \times SE_{diff}$,

```r
me <- t_star * se
me
```

```
## [1] 43.90251
```
The confidence interval is $\bar{x}_{diff} \pm ME_{diff}$,

```r
x_bar_diff + c(-1, 1) * me
```

```
## [1]  14.64749 102.45251
```
