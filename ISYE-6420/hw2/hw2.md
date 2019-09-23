
# HOMEWORK 2
<div style="text-align: right"> nchadha3 (Nitin Chadha) </div>
<div style="text-align: right"> ISyE 6420 </div>
<div style="text-align: right"> September 21, 2019 </div>

---
## Problem 1
---

### Problem 1(a)
For poisson distribution, we have the following formula for observing k events in an interval, where $\lambda$  is the event rate.

$$
f(k = events) = \frac{\lambda^{k} e^{-\lambda}}{k!} \hspace*{6cm} ...1a(a)
$$

Accoding to the question, cell clusters has a Poisson distribution with mean $\lambda = 5$.

Then above equation becomes:
$$
f(k) = \frac{5^{k} e^{-5}}{k!} \hspace*{6cm} ...1a(2)
$$

Here, in our case, k i.e. events corresponds to number of cell clusters.
Using equation-2 to find the percentage of Petri dishes having 0 cell-clusters is:

$$f(k=0) = \frac{5^{0} e^{-5}}{0!} \hspace*{6cm}$$
$$f(k=0) = e^{-5}\hspace*{6cm}$$


We can calulate this in Python:
```
>>> import math
>>> math.exp(-5)
0.006737946999085467
>>> 
```
__Percentage of Petri dishes having 0 cell-clusters is 0.6737 %__

---
### Problem 1(b)
We can find number of Petri Dishes having atleast 1 cell-cluster from Part-(a) of this question

Let k be the number of cell-clusters ( as in part(a)), then

$$P(k >= 1) = 1 - P(k = 0)$$
$$P(k >= 1) = 1 - e^{-5}$$
$$P(k >= 1) = 1 - 0.006737946999085467$$
$$P(k >= 1) = 0.9932620530009145$$



__Ans = 99.326 %__

---
(c)
We can find the percentage of Petri dishes having more than 8 clusters as follows.
Let k be the number of cell-clusters.
$$
f( k > 8 ) = 1 - f( k <= 8) \hspace*{7cm} .. 1c(1)
$$

Since, $f(k <= 8 )$ is a possion distribution, we can use the  cumulative distribution function to find $f( k <= 8)$

$$f(k, \lambda) =  \sum_{i=0}^{k} \frac{e^{-\lambda}*\lambda^i}{i!}  \hspace*{7cm} .. 1c(2)$$
$$f(k, \lambda = 5) =  \sum_{i=0}^{k} \frac{e^{-5} * 5^i}{i!} \hspace*{7cm} .. 1c(3)$$
$$f(k <= 8, \lambda = 5) =  \sum_{i=0}^{8} \frac{e^{-5} * 5^i}{i!} \hspace*{7cm} .. 1c(3)$$
Putting $1c(3)$ in $1c(1)$ we get

$$f( k > 8 ) = 1 - \sum_{i=0}^{8} \frac{e^{-5} * 5^i}{i!} $$
$$f( k > 8 ) = 1 - (e^{-5}*\sum_{i=0}^{8} \frac{5^i}{i!}) $$

I have written a small python code to calculate this as follows:

```
>>> 
>>> def func(k): # given k, return (5^k)/k!
...   return float(5**k)/float(math.factorial(k))
... 
>>> x = map(func, [0,1,2,3,4,5,6,7,8])
>>> x
[1.0, 5.0, 12.5, 20.833333333333332, 26.041666666666668, 26.041666666666668, 21.70138888888889, 15.500992063492063, 9.68812003968254]
>>> y = sum(x)
>>> y
138.30716765873015
>>> 1 - y*math.exp(-5)
0.0680936347218486
>>> 
```

__The percentage of Petri dishes having more than 8 clusters is 6.809%__

---

(d)
Building up on our solution, we can re-use equation $1c(3)$ (cum density function) here.

$$f( 4 <= k <= 6) = f( k <= 6) - f( k < 3)$$
$$f( 4 <= k <= 6) =  \sum_{i=0}^{6} \frac{e^{-5} * 5^i}{i!} - \sum_{i=0}^{3} \frac{e^{-5} * 5^i}{i!}$$
$$f( 4 <= k <= 6) =  e^{-5}( \sum_{i=0}^{6} \frac{ 5^i}{i!} - \sum_{i=0}^{3} \frac{ 5^i}{i!} )$$

Like earlier, using a small python script here:
```
>>> def func2(k):
...   fac = lambda k: float(5**k)/float(math.factorial(k))
...   __sum = sum(map(fac, range(k+1))) # include k
...   return __sum
... 
>>> 
>>> case_6 = func2(6)
>>> case_3 = func2(3)
>>> math.exp(-5)*(case_6 - case_3)
0.497157547675577
>>> 
```
__Answer=49.715%__

---
## Problem 2

<div style="text-align: right"> nchadha3 (Nitin Chadha) </div>
<div style="text-align: right"> ISyE 6420 </div>
<div style="text-align: right"> September 21, 2019 </div>

---
### Problem 2(a)
To find the probability that a run continues for at least 10 hours, we can find the following probability:
Let k = number of hours a run continues, then
$$ f(k >= 10 hours) = 1 - f( k<10) $$
We can use a cumulative distribution function to find $f( k<10)$
Since our distribution is exponential distribution, we have following formula for cdf:
$$ f(k, \lambda) = 1 - e^{-\lambda*k} \hspace*{2cm} k >= 0\hspace*{2cm}.. 2a(1)$$
According to the question, $\lambda=1/10$ and $k=10$ from this part of question.
Putting these respective values in above eq:
$$ f(k >= 10 hours) = 1 - f( k<10) $$
$$ f(k >= 10 hours) = 1 - (1 - e^{-(1/10)*10})) $$
$$ f(k >= 10 hours) =  e^{-1} $$
$$ f(k >= 10 hours) =  0.36787944117144233 $$

__The probabilities that a run continues for at least 10 hours is 36.7879%__

---
### Problem 2(b)
To find the probabilities that a run lasts less than 15 hours, we can directly use the equation in $2a(1)$

$$ f(k, \lambda) = 1 - e^{-\lambda*k} \hspace*{2cm} k >= 0$$
$$ f(k < 15) = 1 - e^{-(1/10)*15}$$
$$ f(k < 15) = 1 - e^{-3/2}$$
$$ f(k < 15) = 1 - e^{-3/2}$$
$$ f(k < 15) = 0.7768698398515702$$

__The probability that a run lasts less than 15 hours is 77.6869%__

---
### Problem 2(c)

Since exponential is a memoryless function [Link](https://en.wikipedia.org/wiki/Memorylessness#The_memoryless_distribution_is_an_exponential_distribution), we can safely write,
$$ Pr(k > s+t | k > t) = Pr(t) $$
Then, the probabilities that a run continues for at least 20 hours, given that it has lasted 10 hours.
$$ Pr(k > 10+10 | k > 10) = Pr(10) $$

Using the result from Problem 2(a), we have 
$$ f(k >= 10 hours) =  0.36787944117144233 $$

__Ans=36.7879%__

---
## Problem 3

<div style="text-align: right"> nchadha3 (Nitin Chadha) </div>
<div style="text-align: right"> ISyE 6420 </div>
<div style="text-align: right"> September 21, 2019 </div>

---
### Problem 3(a)

$$
f(x,y) =
\begin{cases}
\lambda^2 e^{-\lambda y} & \quad 0 \leq x \leq y, & \lambda > 0 \\
0, & \quad \text{else}.
\end{cases}
$$


Let $-\lambda*y = a$, then 

$$
\begin{array}{lcll}
Let -\lambda*y & = & a\\
da/dy & = & -\lambda \\
dy & = & \frac{-1}{\lambda}da \\
 \\
f_X(x) & = & \int_{x}^{\infty} \lambda^2 e^{-\lambda y} dy \\
\\
f_X(x) & = & \int_{x}^{\infty} \lambda^2 e^{a} \frac{-1}{\lambda} da \\
\\
f_X(x) & = & -\lambda \int_{x}^{\infty}  e^{a} da \\
\\
\int_{}{}  e^{a} da & = & e^{a} \hspace*{2cm} .. [A]\\
\\
f_X(x) & = & -\lambda \int_{x}^{\infty}  e^{a} da \\
& = & -\lambda ( e^a \Big|_{x}^{\infty}) da\\
\\
& = & -\lambda ( e^{-\lambda y} \Big|_{x}^{\infty}) dy \hspace*{1cm} Putting\phantom bback\\
\\
& = & -\lambda (e^\infty - e^{-\lambda x}) \\
\\
& = & -\lambda (0 - e^{-\lambda x}) \\
\\
& = & \lambda e^{-\lambda x}
\end{array}
$$
[A] refers to https://www.integral-calculator.com/

PDF of $\mathcal{E}(\lambda)$ is $f(x) = \lambda e^{-\lambda x}$

Our dervied result and above equation for PDF is same.

---
### Problem 3(b)

$$
f(x,y) =
\begin{cases}
\lambda^2 e^{-\lambda y} & \quad 0 \leq x \leq y, & \lambda > 0 \\
0, & \quad \text{else}.
\end{cases}
$$

$$
\begin{array}{lcl}
f_Y(y) & = & \int_{0}^{y} \lambda^2 e^{-\lambda y} dx \\
\\
& = & \lambda^2 e^{-\lambda y} \int_{0}^{y} dx \\
\\
& = & \lambda^2 e^{-\lambda y} x \Big|_{0}^{y} \\
\\
& = &\lambda^2 e^{-\lambda y} y
\\
\end{array}
$$
Now PDF of $\mathcal{G}a(\alpha,\beta)$ is as follows.
$$
\begin{array}{l}
f(x,\alpha,\beta) = \frac{\beta^{\alpha }x^{\alpha -1}e^{-\beta x}}{\Gamma(\alpha )} \quad x, \alpha ,\beta > 0.
\end{array}
$$
According to the question,
$\lambda = \beta$ and $\alpha = 2$

$$
\begin{array}{l}
f(x,2,\lambda) = \frac{\lambda^{2 }x^{2 -1}e^{-\lambda x}}{(2 - 1)!} \\
\\
f(x,2,\lambda) = \frac{\lambda^{2 }xe^{-\lambda x}}{1!} \\
\\
f(x,2,\lambda) = \lambda^{2 }xe^{-\lambda x} \\
\end{array}
$$

Above equation is same as we derived.

---

### Problem 3(c)

$$
\begin{array}{lcl}
f(y|x) & = & \frac{f(x,y)}{f_x(x)} \\
\\
& = & \frac{\lambda^2 e^{-\lambda y}}{\lambda e^{-\lambda x}} \quad from-3(a)\\
\\
& = & \lambda e^{-\lambda y - \lambda x} \\
\\
& = & \lambda e^{-\lambda (y - x)}
\end{array}
$$

---
### Problem 3(d)

$$
\begin{array}{lcl}
f(x|y) & = & \frac{f(x,y)}{f_y(y)} \\
\\
& = &  \frac{\lambda^2 e^{-\lambda y}}{\lambda^{2} y e^{-\lambda y}} \quad from-3(b) \\
\\
& = & \frac{1}{y}
\end{array}
$$
Now,
$$ \mathcal{U}(a,b) = \frac{1}{b-a} $$
$$ \mathcal{U}(0,y) = \frac{1}{y-0} $$
$$ \mathcal{U}(0,y) = \frac{1}{y} $$

Last equation matches our result.

---
## Problem 4

<div style="text-align: right"> nchadha3 (Nitin Chadha) </div>
<div style="text-align: right"> ISyE 6420 </div>
<div style="text-align: right"> September 21, 2019 </div>

---
### Problem 4(a)

A classical statistician would estimate λ using the Maximum Likelihood Estimate

$$ MLE(exponential) = \frac{1}{Mean} $$

$$
Mean = \frac{1}{n} \sum_{i=1}^n X_i = \frac{1}{3} (3 + 13 + 8) = 8.
$$

Thus,

$$
MLE(exponential) = \lambda = \frac{1}{8}.
$$

---

### Problem 4(b)

what is the Bayes estimator of λ if the prior is π(λ)=1/√λ, λ>0?

Hint: In (b) the prior is not a proper distribution, but the posterior is. Identify the posterior from the product of the likelihood from (a) and the prior, no need to integrate.

We know
$$Posterior ∝ Likelihood × Prior$$
Here,
cumulative density function is defined as follows for exponential eq:
$$ f(x, \lambda) = \lambda e^{-\lambda x} $$
And 
$$ Prior = \pi(\lambda) = \lambda^{-1/2} $$
And, [Likelihood](https://en.wikipedia.org/wiki/Exponential_distribution#Parameter_estimation)
$$ F(\lambda, x_1, x_2, x_3, ...) = \lambda^n e ^{-\lambda \sum_{i=1}^{n} x_i} $$

Using above equations, we have

$$
\begin{array}{lcl}
Posterior ∝ Likelihood \times Prior \\
& \propto &  \lambda^n e ^{-\lambda \sum_{i=1}^{n} x_i}  \times \lambda^{-1/2}\\
& \propto &  \lambda^3 e ^{-24\lambda}  \times \lambda^{-0.5} \quad (From 4(a)) \\
& \propto &  \lambda^{2.5} e ^{-24\lambda}  
\end{array}
$$

For Maximum Likelihood Estimate, we need to take derivate.
So:
$$
\frac{d( \lambda^{2.5} e ^{-24\lambda})}{d\lambda} = 0
$$
using [online calculator](https://www.derivative-calculator.net), 

$$
\frac{5\lambda^{3/2}e^{-24\lambda}}{2} - 24\lambda^{5/2}e^{-24\lambda} = 0 \\
\frac{5\lambda^{3/2}e^{-24\lambda}}{2} = 24\lambda^{5/2}e^{-24\lambda} \\
\\
5\lambda^{3/2}e^{-24\lambda} = 48\lambda^{5/2}e^{-24\lambda} \\
\frac{5}{48} = \lambda^{2/2} \\
\lambda = 0.10416666666666667
$$


__Ans = 0.1045__

---