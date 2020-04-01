# Life expectancy prediction using BART
Using the <a href="https://github.com/JingyuHe/XBART/tree/master/python">bartpy package</a> to predict life expectancy (World Bank) from income distribution data (WID.world)

<a href = "https://arxiv.org/abs/0806.3286"> BART (Bayesian Additive Regression Trees) (Chipman et al. 2008)</a> uses a sum of trees to approximate the function mean (as with GBT methods), but uses a prior to regularise the fit to keep the individual tree effects small ("weak learners"), thus favouring simpler trees. The inference is performed using MCMC sampling, so we are able to obtain Bayesian <b>error estimates</b> alongside our predictions.

By using a Bayesian method, most of the hyperparameter training is done within the algorithm (except the number of trees due to computational concerns, although values seem to be robust to this at m = 200). The priors themselves consist of three sub-priors: tree structure, values in terminal nodes and residual noise. In his <a = href = "https://towardsdatascience.com/bayesian-additive-regression-trees-paper-summary-9da19708fa71">blog post</a>, Zak Jost explains the jist of the MCMC algorithm in his blog post:

<blockquote>"Pick a tree in the additive sequence, morph it by randomly choosing among some rules (PRUNE, GROW… etc), from this new tree, sample from the terminal node value distribution, then choose whether to keep this new tree or the original according to their ratio of posterior probabilities."</blockquote>

The bartpy package iteself is super slow as the sampling is entirely written in python, but it can be used with sklearn working, making it easy for direct comparison.
