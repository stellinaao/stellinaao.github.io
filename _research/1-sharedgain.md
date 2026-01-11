---
title: "Changes in Shared Neural Activity Across the Lifespan"
excerpt: "Does the shared activity between corticostriatal circuits change as mice age? Could such a change explain age-related shifts in decision-making strategies?"
collection: research
permalink: /research/sharedgain
venue: "UCLA"
redirect_from:
  - /1-sharedgain
---
For those treading the alleys of age, it may be comforting to know that an elderly mouse performs just as well as her juvenile counterpart on a mildly challenging decision-making task (everyone flounders on the challenging task). Still, young and old mice make decisions differently. Younger mice tend to be model-based: the gifted rodent learns that the spout with his water reward switches every five trials, remembers that he has been rewarded on the left spout for the past five trials, and thus predicts that the probability of the right spout being rewarded is mighty high. For the psychologists, model-based decision making is similar to goal-directed decision making; for the quantitative aficionados, we liken model-based decision making to Bayesian inference. Older mice have a hard time staying model-based, and more often adopt a model-free strategy. The wizened mouse updates action-value pairs based on recent history: she continues to lick to the right as long as she is rewarded, increasing the value of a right lick; upon a block switch, she immediately devalues the right lick. This behavior is reminiscent of the win-stay lose-switch strategy observed in psychology, and is modeled with Q-learning.

Parallel corticostriatal circuits underlie these two strategies; abstracting nuance, projections from the anterior cingulate cortex (ACC) to the dorsal medial striatum (DMS) support model-based behavior, while projections from the secondary motor cortex (M2) to dorsal lateral striatum (DLS) support model-free behavior. But what mediates the shift from model-based to model-free behavior with age? The neurons in the model-based circuit don’t wither away; instead, do the computations performed by the two circuits change?

To interpret the cacophony of spikes from hundreds of neurons, it is helpful to model the data with a reduced set of variables. Relating two latent variables to abstract phenomena like attention and strategy is significantly simpler than extracting meaning from the babbling of 500 cells. Furthermore, we can enforce biologically-informed constraints to make the latent variables easier to interpret. For example, the Generalized Affine Model defines latents to have either a multiplicative or additive effect on a neuron’s tuning curve. We can formalize this relationship with the following equation, where \\(r_i^n\\) is the nth neuron’s firing rate on trial \\(n\\), \\(g_i^k\\) is the value of multiplicative latent \\(k\\) on the trial \\(i\\), and \\(h_i^m\\) is the value of additive latent \\(m\\) on trial \\(i\\). Independent of the trial, \\( w_n^k \\) is the coupling coefficient of neuron \\(n\\) to multiplicative latent \\(k\\), \\(b_n\\) is a bias term, \\(f_n(\theta)\\) is the average response of neuron \\(n\\) to stimulus \\(\theta\\), and \\(v_n^m\\) is the coupling coefficient of neuron \\(n\\) to additive latent \\(m\\).

$$r_i^n = (\sum_{k=1}^Kw_n^kg_i^k+b_n)f_n(\theta)+\sum_{m=1}^Mv_n^mh_i^m$$


Note that the function relating population spiking activity to the latents has no constraints, and is fit by maximizing log-likelihoods with an autoencoder.

Importantly, forcing the latents to either have a multiplicative or additive effect on the firing rate grounds them with biologically-plausible explanations. For example, a multiplicative latent time series shared among all neurons could indicate a shared modulator, such as attention, arousal, movement, or, in our case, strategy. We can test this hypothesis by correlating strategy, defined for each trial with a state-space model, with each of the multiplicative latents. 

More broadly, creating a reduced model of population activity allows us to use more nuanced analyses to determine whether strategy acts as shared gain on corticostriatal circuit activity and how its effects change across age.