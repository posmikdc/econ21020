# Overview

We are moving from the basics of Statistics to the exciting world of regression. This week, we will spend some time internalizing some of the concepts we have learned about, especially identification, the analogy principle and method of moments, and regression basics. 

Rest assured, that even if you currently feel like this ...  

<img src="https://i.kym-cdn.com/entries/icons/original/000/046/895/huh_cat.jpg"/> 

... we will get through this together! 


## Method of Moments and Analogy 



## Identification 

### A quick review 

Let us recall the definition from your lecture slides: 

**Let the data have a parametric distribution $f_{Y,X}(\cdot; \theta)$. The parameter $\theta$ is identified if it can be written exclusively as a function of the moments of the distribution of the data (i.e., of population data moments (PDM))**

A couple of notes on this definition: 

- **A "parametric distribution":** 
    - For our purposes, think of these parametric distribution necessitating two ingredients: Data and the parameters that are meant--as a function of data--to generalize them 
- **"Moments":**  
    - This definition is why it is important to know about the method of moments and the analogy principle
    - Rest assured, working knowledge is fine 
- **"A function of the moments":** 
    - Basically, this says that the data is sufficient or powerful enough to fully and uniquely characterized by our data
    - Moments are a statistical theorists way to characterize our data in different ways, i.e. a first moment $\mathbb{E}(X)$ characterizes where a distribution is centered, a second moment $\mathbb{E}(X^2)$ characterizes how spread out data is. Higher moments characterize different things, such as skewness and kurtosis. 
    - Truth be told, I have never heard anyone use anything higher than a fourth moment, the heaviness of a distributions tail "Kurtosis", although a 5th and 6th moment exist in practice.  

Now, let us take a look at Ex. 5d on PSet 2. It is on the technical side, so I want to make sure we can tie its learning objectives into the intuition you are building. 

From Definition 2 on PSet 2, we have: 

**Consider a RV $X$ with CDF $F(\cdot; \theta)$. We do not know the number $\theta$ but we know that it belongs to set $\Theta$. We say that the parameter $\theta$ is identified if $F(x;\theta') = F(x;\theta'')$ for all $x$ in the support of the CDF implies $\theta' = \theta''$ for all $\theta',\theta'' \in \Theta$. We say that the parameter $\theta$ is not identified if $\exists~\theta', \theta '' \in \Theta$ such that $F(x;\theta') = F (x;\theta'')$ for all $x$.**

Again, let us dive deeper into what this means: 

- **"the number of $\theta$": 
    - This is really important to understand. Different distributions are parametrized by different parameters and also by a different number of parameters. For example, our normal distribution is parametrized by two parameters, mean $\mu$ and variance $\sigma^2$. Meanwhile, the exponential distribution is only parametrized by one so-called "rate parameter", $\lambda$
- **"if $F(x;\theta') = F(x;\theta'')$":**
    - This is an important formalization of the identification requirement. Given the same data, we only want one set of parameters to map onto one cumulative chunk of probability mass 
    - If this equality is true (no identification), our CDF would not be monotonic (Cannot exist) 
    - If this equality is not true (that's when we have identification), our CDF is indeed monotonically increasing (Awesome)
    - Think: We want our parameters to be **unique** functions of our data. If we don't have this 1-to-1 mapping, we cannot uniquely identify our parameter via a combination "of the moments of the distribution of the data" 
    - So when formally checking whether a set of parameters is not identifiable, we can just check whether this equality is true! 

### PSet 2, Ex. 5d 

So, let's apply these thoughts to PSet 2, Exercise 5d 

We are interested in seeing whether the set of parameters $\theta = (\beta_0, \beta_1, \mu, \sigma^2)$ are identified in our non-linear model:  

$$
Y = 1(\beta_0 + \beta_1 X - U \leq 0)
$$

In the previous part of the exercise, we have derived: 

$$ 
Pr(Y = 1 | X = x, \theta) = Pr(1[\beta_0 + \beta_1 X - U \leq 0] = 1 | X = x) = \cdots = \Phi(\frac{\beta_0 + \beta_1 X - \mu}{\sigma})
$$

For simplicity in the later calcululation, we can simply rearrange as: 

$$
\Phi(\frac{\beta_0 + \beta_1 X - \mu}{\sigma}) = \Phi(\frac{\beta_0 - \mu}{\sigma} + \frac{\beta_1 X}{\sigma}) 
$$

Now, we can pick any two values for $\theta = (\beta_0, \beta_1, \mu, \sigma^2)$ and $\theta' = (\beta_0, \beta_1', \mu', \sigma^{2}~')$ such that: 

- $\theta \neq \theta'$
- $\frac{\beta_0 - \mu}{\sigma} = \frac{\beta_0' - \mu'}{\sigma'}$ 
- $\frac{\beta_1 X}{\sigma} = \frac{\beta_1' X}{\sigma'}$

We split up our pevious equation to state this condition more easily. You can pick _any_ values that meet these conditions, no need to overcomplicate. They just need to be different but equal in the latter two conditions. 

Now, we can verify: 

$$
Pr(Y = 1 | X = x;\theta) = \Phi(\frac{\beta_0 - \mu}{\sigma} + \frac{\beta_1 X}{\sigma}) = \Phi(\frac{\beta_0' - \mu'}{\sigma'} + \frac{\beta_1' X}{\sigma'}) = Pr(Y = 1 | X = x;\theta') 
$$

If you can find parameters $\theta \neq \theta'$ such that this equivalence relation is met, you can conclude that identification is not possible! (Spoiler alert: I have a feeling you will be able to)

### Normalization can lead to Identification 

Now, since you have concluded that identification is not possible, is there something you can do about it? 

_The answer is yes._

Although our four parameters $\theta = (\beta_0, \beta_1, \mu, \sigma^2)$ cannot be identified, we can do something to transform our four parameters into two. We can consider $\frac{\beta_0 - \mu}{\sigma}$ and $\frac{\beta_1 X}{\sigma}$ as so-called **composite parameters**. Although this may seem as strange as it does arbitrary, you have actually seen this thought before in z-score normalization. 

As a matter of fact, we can do exactly this here: Normalize our composite parameters to achieve identification. 

Indeed, ($\frac{\beta_0 - \mu}{\sigma}, \frac{\beta_1 X}{\sigma})$ are identified because $\Phi(\cdot)$ is a monotonic function. You can check why this works if you back to the previous exercise and verify that we cannot repeat it. **A quicker way to get to this result is to realize that we have two unknown (composite) parameters and two equations, so we can achieve identification!** This is actually how you would usually proceed when dealing with linear equations, i.e. verify we have at least as many identifying equations (i.e. analogy principle) as we have parameters. "Only" in the non-linear case do we have to proceed more carefully and rigorously, as seen above. 

In this case, given the normalization we can say: 

$$
(\frac{\beta_0 - \mu}{\sigma}, \frac{\beta_1}{\sigma}) = (\beta_0, \beta_1)
$$

where $X$ is not a parameter but rather data and we can think of the mean term in the second component as 0. Looking at this you may already see why normalization offers itself so well here. 

I know this may seem a bit arbitrary. But since many of you may see a normalization in action for the first time, I would try to focus on understanding on why it works first. Then, realize that you will be able to actually recognize when this is a good idea once you build on your statistical intuition. 



