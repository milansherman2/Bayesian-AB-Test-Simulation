# Bayesian-AB-Test-Simulation
Estimating time to significance using Bayesian sampling

<h2>Overview</h2>
<p>
One of the primary roles that I filled while working at Bestow is the design and analysis of A/B tests of new products and user experience in conjunction with our product team.  However, a challenge that we faced at Bestow is that the volume of traffic we had moving through our funnel was too low to make traditional A/B testing practical.  I completed a Udemy course on Bayesian A/B testing using python (https://www.udemy.com/course/bayesian-machine-learning-in-python-ab-testing/), and conducted additional research to prepare a presentation on the advantages of the Bayesian approach.  The tl;dr version of the presentation is as follows:
  </p>

<b>Traditional A/B Testing</b>:
- Does not answers the question, “what is the probability that A  > B?”
- Requires larger samples
- Unlikely to detect incremental lifts
- Wastes money 
- Often inconclusive, i.e., 'fail to reject the null hypothesis' only says that we don't have enough evidence to reject the null hypothesis, it makes no claim about which variant is better.

<b>Bayesian A/B Testing</b>:
- Answers the question, “what is the probability that A > B?”
- Can quantify risk with smaller lifts and smaller sample
- Minimizes wasted spend 
- Flexible when deciding when to end an experiment and declaring a winner

<b>Code</b>:
The code included adapts code from the course to run a simulation of an experiment.  The code that defines the classes and generates the visualization is from the course, adapted to this specific context.  The question I was trying to answer is how long it would take to achieve a particular level of certainty about the which variation is better.  The genious of Bayesian sampling is that the variants are sampled based on their success, i.e., a variant will be sampled more frequently if it demonstrates a better conversion rate.  This prevents wasting time and money continuing to serve users an inferior version of a product or experience, while simultaneously checking what is assumed to be the inferior version to make sure that it indeed is inferior.

The particular experiment I am simulating with this code are two variations of a user experience, one that results in a 21% conversion rate (the baseline or control version), and another that has a 25% conversion rate.  In reality, we don't know this conversion rate, but we're assuming it will be better than the control as that's the point of designing a new product.  What the simulation shows is how often the better variant will actually "win" if the conversion rate is 25%.  Because the sampling algorithm is "greedy", early wins by the inferior variant can result in that variant being sampled more frequently initially and appearing to be the better variant.  However, as each variant continues to be sampled, each should begin to converge to their theoretical distributions.  The question is how long that will take.  In this code, I run an experiment 10,000 times with 500 trials, i.e., after sampling from both variants a total of 500 times, which variant has the larger conversion rate?  After doing this 10,000 times, how often does the better variant come out on top?  Then I repeat this for trials of 600, 700, 800, 900, and 1000.  As expected the better variant comes out on top a larger proportion of the time as the number of trials increases.  I then compare this with a power analysis to determine the sample size needed for a variety of p-values, i.e, p=.2, .1, .05, and .01.  It is important to remember that this is simply the sample needed to have a valid A/B test in the traditional fraemework.  




