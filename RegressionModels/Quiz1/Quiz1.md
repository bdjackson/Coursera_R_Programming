# Quiz 1


```r
library(datasets)
```

## Question 1
Consider the data set given below


```r
x <- c(0.18, -1.54, 0.42, 0.95)
```

And weights given by


```r
w <- c(2, 1, 3, 1)
```

Give the value of μ that minimizes the least squares equation.

Answer:

```r
sum(w*x)/sum(w)
```

```
## [1] 0.1471429
```


## Question 2
Consider the following data set


```r
x <- c(0.8, 0.47, 0.51, 0.73, 0.36, 0.58, 0.57, 0.85, 0.44, 0.42)
y <- c(1.39, 0.72, 1.55, 0.48, 1.19, -1.59, 1.23, -0.65, 1.49, 0.05)
```
Fit the regression through the origin and get the slope treating y as the
outcome and x as the regressor. (Hint, do not center the data since we want
regression through the origin, not through the means of the data.)

Answer:

```r
sum(x*y)/sum(x*x)
```

```
## [1] 0.8262517
```

We can test this using the linear model function in R

```r
lm(y~x+0)
```

```
## 
## Call:
## lm(formula = y ~ x + 0)
## 
## Coefficients:
##      x  
## 0.8263
```

## Question 3
Do data(mtcars) from the datasets package and fit the regression model with mpg as the outcome and weight as the predictor. Give the slope coefficient.

Answer:

```r
data(mtcars)
```


```r
lm(mtcars$mpg ~ mtcars$wt)
```

```
## 
## Call:
## lm(formula = mtcars$mpg ~ mtcars$wt)
## 
## Coefficients:
## (Intercept)    mtcars$wt  
##      37.285       -5.344
```


## Question 4
Consider data with an outcome (Y) and a predictor (X). The standard deviation
of the predictor is one half that of the outcome. The correlation between the
two variables is .5. What value would the slope coefficient for the regression
model with Y as the outcome and X as the predictor?

Answer:
Let's start with some basic equations
$$
cor(x,y) = \frac{cov(x,y)}{S_x S_y} \\
cov(x,y) = \frac{1}{n-1}\sum_{i} (x_i - \bar{x})(y_i - \bar{y}) \\
S_x^2 = \frac{1}{n-1}\sum_{i} (x_i - \bar{x})^2 \\
$$

From the problem statement, we know,
$$
S_y = 2S_x \\
cor(x,y) = 0.5 \\
y_i = m*x_i \\
$$

We can rewrite a few of our above equations:
$$
S_xS_y = 2S_x^2 = 2\frac{1}{n-1}\sum_{i} (x_i - \bar{x})^2 \\
$$
$$
\begin{aligned}
\bar{y} & = \frac{1}{n}\sum_i y_i \\
& = \frac{m}{n}\sum_i x_i \\
& = m\bar{x} \\
\end{aligned}
$$
$$
\begin{aligned}
cov(x,y) & = \frac{1}{n-1}\sum_{i} (x_i - \bar{x})(mx_i - m\bar{x}) \\
& = \frac{m}{n-1}\sum_{i} (x_i - \bar{x})^2 \\
& = mS_x^2 \\ 
\end{aligned}
$$

Now, we can rewrite the equation for the correlation
$$
\begin{aligned}
cor(x,y) & = \frac{cov(x,y)}{S_x S_y} \\
& = \frac{mS_x^2}{2S_x} \\
& = \frac{m}{2} \\
\end{aligned}
$$
$$
cor(x,y) = 0.5 = \frac{m}{2} \\
m = 1 \\
$$

## Question 5
Students were given two hard tests and scores were normalized to have empirical
mean 0 and variance 1. The correlation between the scores on the two tests was
0.4. What would be the expected score on Quiz 2 for a student who had a
normalized score of 1.5 on Quiz 1?

Answer:
Let's start by writing down what we know
$$
\bar{x_1} = \bar{x_2} = \bar{x} = 0 \\
s_{x_1} = s_{x_2} = s = 1 \\
cor(x_1, x_2) = 0.4 \\
$$

$$
\begin{aligned}
cor(x_1, x_2) & =
\frac{1}{n-1}
\frac{\sum_i (x_{1i} - \bar{x_1})(x_{2i} - \bar{x_2})}
{s_{x_1}s_{x_2}} \\
& = \frac{1}{n-1} \sum_i x_{1i}x_{2i} \\
\end{aligned}
$$

We can construct the expected relation
$$
x_{1i} = \gamma x_{2i}
$$

$$
\begin{aligned}
cor(x_1, x_2)
& = \frac{1}{n-1} \sum_i x_{1i}\gamma x_{1i} \\
& = \frac{1}{n-1} \gamma \sum_i x_{1i}^2 \\
& = \gamma s \\
\end{aligned}
$$

This means that $\gamma = cor(x_1,x_2)$


```r
cor <- 0.4
x1 <- 1.5
gamma <- cor
x2 <- gamma*x1
x2
```

```
## [1] 0.6
```


## Question 6
Consider the data given by the following


```r
x <- c(8.58, 10.46, 9.01, 9.64, 8.86)
```

What is the value of the first measurement if x were normalized (to have mean 0
and variance 1)?

Answer:

```r
(x[1]-mean(x))/sd(x)
```

```
## [1] -0.9718658
```

## Question 7
Consider the following data set (used above as well). What is the intercept for fitting the model with x as the predictor and y as the outcome?


```r
x <- c(0.8, 0.47, 0.51, 0.73, 0.36, 0.58, 0.57, 0.85, 0.44, 0.42)
y <- c(1.39, 0.72, 1.55, 0.48, 1.19, -1.59, 1.23, -0.65, 1.49, 0.05)
```

Answer:

```r
lm(y~x)
```

```
## 
## Call:
## lm(formula = y ~ x)
## 
## Coefficients:
## (Intercept)            x  
##       1.567       -1.713
```

## Question 8
You know that both the predictor and response have mean 0. What can be said about the intercept when you fit a linear regression?

Answer:
The intercept will be exactly zero.

## Question 9
Consider the data given by


```r
x <- c(0.8, 0.47, 0.51, 0.73, 0.36, 0.58, 0.57, 0.85, 0.44, 0.42)
```
What value minimizes the sum of the squared distances between these points and
itself?

Answer:
The mean of the values minimizes the squared distance between the points and
itself

```r
mean(x)
```

```
## [1] 0.573
```


## Question 10
Let the slope having fit Y as the outcome and X as the predictor be denoted as
β1. Let the slope from fitting X as the outcome and Y as the predictor be
denoted as γ1. Suppose that you divide β1 by γ1; in other words consider β1/γ1.
What is this ratio always equal to?

Answer:
Let us consider the equations we get when fitting Y as an outcome of X and X as
an outcome of Y.

$$
f(x) = \beta_1 x \\
g(x) = \gamma_1 y \\
$$

To perform the fit, we want to minimize the following equations:
$$
s_y = \sum_i \left(y_i - f(x_i)\right)^2 
= \sum_i \left(y_i - \beta_1 x_i\right)^2 \\
s_x = \sum_i \left(x_i - g(y_i)\right)^2 
= \sum_i \left(x_i - \gamma_1 y_i\right)^2 \\
$$

These are pretty much the same, so let's work with $s_y$.
$$
\begin{aligned}
\frac{\partial s_y}{\partial \beta_1} 
& = -2 \sum_i \left(y_i - \beta_1 x_i \right) x_i \\
& = -2 \left(\sum_i x_i y_i - \beta_1 \sum_i x_i^2 \right) \\
\end{aligned}
$$

We are minimizing, so we will set the derivative to zero
$$
\begin{aligned}
0 & = -2 \left(\sum_i x_i y_i - \beta_1 \sum_i x_i^2 \right) \\
\sum_i x_i y_i & = \beta_1 \sum_i x_i^2 \\
\beta_1  & = \frac{\sum_i x_i y_i}{\sum_i x_i^2} \\
\end{aligned}
$$

Similarly,
$$
\gamma_1 = \frac{\sum_i x_i y_i}{\sum_i y_i^2}
$$

Taking the ratio $\beta_1/\gamma_1$
$$
\begin{aligned}
\frac{\beta_1}{\gamma_1} & = 
\frac{\frac{\sum_i x_i y_i}{\sum_i x_i^2}}
{\frac{\sum_i x_i y_i}{\sum_i y_i^2}} \\
& = \frac{\sum_i x_i y_i}{\sum_i x_i y_i} \frac{\sum_i y_i^2}{\sum_i x_i^2} \\
& = \frac{\sum_i y_i^2}{\sum_i x_i^2} \\
& = \frac{\mathrm{var}(Y)}{\mathrm{var}(X)}
\end{aligned}
$$

We can take the last step because we already stated both X and Y had means of
zero.
