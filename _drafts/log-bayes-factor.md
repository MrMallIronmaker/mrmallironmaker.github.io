My thought process:

Let's get the bayes factor \frac{P(d|h_{1})}{P(d|h_{0})}
, into some intuition. First, what is it? So there are rules of thumb - values like 1 mean that the evidence is just as good for one as for the other. Evidence around a 3 or 1/3 is “anecdotal” and evidence around 10 or 1/10 is fairly strong. Also, the factors work in a multiplicative way - if you have one set of data with Bayes factor of 10, and another set of data with a BF of 3, then if you put the data together you get a factor of 30. Immediately I start thinking that maybe we should be working linearly - so let's use logarithms! What if we take \log\frac{P(d|h_{1})}{P(d|h_{0})}
? Our “anecdotal” level is now \pm1.1
, and our scientific level is \pm2.3
.

What should we compare it to? Lately, I've been fooling around with effect size (Cohen's d) as a first-order measure of effect size. Let's use that and convert particular values of effect size to bayes factors.

So we have two possible hypotheses, h_{0}
and h_{1}
, and some data that might fit either, d
. Let's consider P(d|h_{0})
, but really they can be computed similarly. Approximating the data with its mean and standard deviation, we can create a distribution for it. The total probability is the integral of their product, i.e:

P(d|h_{0})=\int_{-\infty}^{\infty}\mathcal{N}(x|\mu_{0},\sigma^{2})\mathcal{N}(x|\mu_{d},\sigma^{2})


Expanding out the definition of the normal function, we have:

P(d|h_{0})= \int_{-\infty}^{\infty}\mathcal{N}(x|\mu_{0},\sigma^{2})\mathcal{N}(x|\mu_{d},\sigma^{2})dx
=   \int_{-\infty}^{\infty}\frac{1}{\sqrt{2\pi\sigma^{2}}}e^{-\frac{(x-\mu_{0})^{2}}{2\sigma^{2}}}\frac{1}{\sqrt{2\pi\sigma^{2}}}e^{-\frac{(x-\mu_{d})^{2}}{2\sigma^{2}}}dx
=   \int_{-\infty}^{\infty}\frac{1}{2\pi\sigma^{2}}e^{-\frac{(x-\mu_{0})^{2}}{2\sigma^{2}}-\frac{(x-\mu_{d})^{2}}{2\sigma^{2}}}dx


Messy! What can we do to clean up? Well, we can normalize our distributions so that \mu_{d}=0
and \sigma^{2}=1
. It's just choosing a midpoint and scaling factor. It also means that \mu_{0}
and \mu_{1}
are now exactly their corresponding Cohen's d. This is now simple enough for Wolfram Alpha to compute.

P(d|h_{0})=  \int_{-\infty}^{\infty}\frac{1}{2\pi\sigma^{2}}e^{-\frac{(x-\mu_{0})^{2}}{2\sigma^{2}}-\frac{(x-\mu_{d})^{2}}{2\sigma^{2}}}dx
=    \int_{-\infty}^{\infty}\frac{1}{2\pi}e^{-\frac{(x-\mu_{0})^{2}}{2}-\frac{x^{2}}{2}}dx
=    \frac{1}{2\sqrt{\pi}}e^{\frac{-\mu_{0}^{2}}{4}}


Now, let's put together both sides of that original bayes factor:

\frac{P(d|h_{1})}{P(d|h_{0})}=   \frac{\frac{1}{2\sqrt{\pi}}e^{\frac{-\mu_{1}^{2}}{4}}}{\frac{1}{2\sqrt{\pi}}e^{\frac{-\mu_{0}^{2}}{4}}}
=    \frac{e^{\frac{-\mu_{1}^{2}}{4}}}{e^{\frac{-\mu_{0}^{2}}{4}}}
=    e^{\frac{-\mu_{1}^{2}}{4}-\frac{-\mu_{0}^{2}}{4}}
=    e^{\frac{\mu_{0}^{2}-\mu_{1}^{2}}{4}}


Pretty elegant! But wait, it gets better. Recall that the bayes factor works multiplicatively, and so we wanted a logarithm of that probability shift.\log\frac{P(d|h_{1})}{P(d|h_{0})}= \log e^{\frac{\mu_{0}^{2}-\mu_{1}^{2}}{4}}
=    \frac{\mu_{0}^{2}-\mu_{1}^{2}}{4}


Wow! Now that is pretty great.

How does it compare to effects I've see recently? For example, I ran a study that had a fairly large Cohen's d of 0.88. So that will be the difference between h_{0}
and the data, but what would the other hypothesis h_{1}
I would have come up with? I think I would have based it on the most similar paper [but maybe tone down the effect some] and would have guessed a mean, oh, I don't know, about 0.2 standard deviations lower than what I found. So I can set up the equation \mu_{0}=0.88,\mu_{1}=0.2
 and calculate the expected log bayes factor for each participant:

 \frac{\mu_{0}^{2}-\mu_{1}^{2}}{4}=\frac{0.88^{2}-0.2^{2}}{4}=0.18
  

 Now multiplying that by the number of observations, 27, I get a total LBF of the study of 4.86, about “twice” as good as “scientific”
