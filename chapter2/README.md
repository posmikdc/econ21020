# Overview

We are moving from the basics of Statistics to the exciting world of regression. This week, we will spend some time internalizing some of the concepts we have learned about, especially identification, the analogy principle and method of moments, and regression basics. 

Rest assured, that even if you currently feel like this ...  

<img src="https://i.kym-cdn.com/entries/icons/original/000/046/895/huh_cat.jpg"/> 

... we will get through this together! 


## Method of Moments and Analogy 

### Population moments 

You can think of moments with the following analogy: 

Suppose you want to describe your dream house to somebody. You may talk about the color of the house, the size, certain features, etc. Particularly, let's say you want to convey that you particularly love houses that have a light color. You may use analogies to describe the color, i.e. you might say something like "I like a house that radiates a happy vibe". 

In method of moments, your house is some data $X$ and you want to summarize certain features about the data. The first moment is the mean, the second moment is the variance (spread) of the data, the third moment is the skewness, the fourth moment is the kurtosis, etc. 

### The Analogy principle

Now, these are population moments. Think about them as when you are touring your house and you see all the things you like, but the person you are describing the house to is not there with you. You need to come up with summaries about the house, i.e. the color is light, to convey the general idea of the house to the person without them actually being there. That is what the analogy principle represents. 

In the sense of the analogy principle, you are equating the population moment with a sample moment/ sample analogue. We do this because it is not possible to estimate population moments without ... well ... having access to the entire population. The sample moments "estimate" the population moments. 

For instance, our sample mean $\bar{X}$ is the sample moment for our population mean $\mathbb{E}(X) = \mu$. 

In a nutshell, the analogy principle enables us to describe properties of our data without having access to the entire population. That is very, very important and powerful. In a way, it is so intuitive that making this thought explicit could confuse you by itself. Like of course we don't have access to all population data points, so naturally we work with sample analogues. 

### Setting up an Example (PSet 2, Q6)

Our setup is as follows: Suppose we have iid data $\{X_1, X_2, \cdots, X_n\}$ s.t. $X_i \sim \mathcal{N}(\theta_1, \theta_2)$. Write out the method of moments estimators for $\theta_1, \theta_2$. 

Note that our "theoretical" (In the population sense) **about the origin** are given by:

- $\mathbb{E}(X_i) = \theta_1$
- $\mathbb{E}(X_i^2) - [\mathbb{E}(X_i)]^2 := \text{Var}(X_i) = \theta_2$

Note that the expression for the variance is as derived as follows because we are taking the second moment **about the origin**. Naturally, if you have $\mathbb{E}(X_i) = 0$, i.e. a distribution centered at zero (that requires a mean parameter), we _could_ just write $\mathbb{E}(X^2) = \theta_2$. You will see this sometimes and I don't want you to get confused, that's why I am mentioning it. 

Now, to compute the method of moments estimators we can just equate (by the analogy principle): 

- $\mathbb{E}(X_i) = \theta_1 \implies \hat{\theta}_1^{MM} = {1/n} \sum_{i=1}^{n} X_i$ 
- $\mathbb{E}(X_i^2) - [\mathbb{E}(X_i)]^2 := \text{Var}(X_i) = \theta_2 \implies \hat{\theta}_2^{MM} = {1/n} \sum_{i=1}^{n} X_i^2 - \left(\frac{1}{n} \sum_{i=1}^{n} X_i \right)^2$

Boom, done! 

### Visualizing the first moment

<img src="http://misswise.weebly.com/uploads/1/8/2/0/18209119/7133605.jpg?418"> 

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

In general, on a fundamental level, note that identification $\neq$ statistical estimation. It is a logical step that needs to be given before estimation even starts. 

<img src="https://causalinference.gitlab.io/assets/Figures/Chapter3/Ch3_Fig_IV.png">

### An Example: PSet 2, Ex. 5d 

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



