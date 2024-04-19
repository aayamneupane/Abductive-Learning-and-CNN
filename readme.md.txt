**Setup**

Please run the code on Colab, some minor modifications need to be made if runnning locally. These modifications have been mentioned in the comments. Also, the output produced is more readable on Colab.

Please upload the file 'dataset.zip' to your Google Drive, inside a folder called AbductiveLearning.

Then, please mount your GDrive before executing. GPU runtime is recommended. The code takes a while to run (approx 1-2 hrs).

If there is an unexpected result for any experiment, please try running the particular module once again. The model may have reached a bad local minima. The loss curves for each experiment are at the bottom of the output. They are also saved to Tensorboard

**Summary**

Perception and reasoning are two representative abilities of intelligence that are integrated seamlessly during human problem-solving processes. In the area of artificial intelligence (AI), the two abilities are usually realised by machine learning and logic programming, respectively.

Abductive learning is targeted at unifying the two AI paradigms in a mutually beneficial way, where the machine learning model learns to perceive primitive logic facts from data, while logical reasoning can exploit symbolic domain knowledge and correct the wrongly perceived facts for improving the machine learning models.

The primary difficulty lies in the fact that the sub-symbolic and symbolic models can hardly be trained together. More concretely: 1) the machine learning model does not have any ground-truth of the labels for training 2) if the machine learning model does not predict the labels accurately, the reasoning model can hardly deduce the correct output or learn the right logical theory.

Given observed facts and background knowledge expressed as first-order logical clauses, logical abduction can abduce ground hypotheses as possible explanations to the observed facts. Thus, it can be used to guess the missing information, for example, logic clauses that complete the background knowledge, or the appropriate labels for the Machine Learning function. These labels can then be used to train the Machine Learning model.

Abductive Learning (ABL) tries to maximise the consistency between the abduced hypotheses H with training data D = {<x1,y1>,<x2,y2>....<xN,yN>}, given background knowledge B. It can be defined as

Con(H ∪ D; B)= max |Dc|, where Dc⊆D

s.t. ∀ <xi,yi> ∈ Dc (B ∪ ∆ ∪ p(xi) |= yi).

where ∆ is a set of abduced logical clauses.

ABL needs to correct the wrongly perceived pseudo-labels to achieve consistent abductions, such that ∆C can be consistent with as many as possible examples in D. Here we denote the labels to be revised as δ[p(X)] ⊆ p(X), where δ is a heuristic function to estimate which labels are perceived incorrectly. Then, logical abduction can be used to find a set of revised labels.

The algorithm used in Abductive Learning can be described as follows:

Initialize a Machine Learning Model p
For N epochs do:
Sample a batch D' from the Dataset D.
Get a set of labels p(x) ∀ x
Use gradient-free optimization methods to find the set of labels to be revised
Abduce a set of logical clauses ∆ and a set of revised labels ∆p, which maximize Con(Hδ ∪ D; B)
Retrain the Machine model on the updated labels.


** Experiments **
Task 1: Handrittwen Equation Dicipherment
In this task, equations are constructed from images of symbols (“0”, “1”, “+” and “=”), and they are generated with unknown operation rules, each example is associated with a label that indicates whether the equation is correct. A machine is tasked with learning from a training set of labelled equations, and the trained model is expected to predict unseen equations correctly. Thus, the machine needs to learn image recognition (perception) and mathematical operations for calculating the equations (reasoning) simultaneously. The images for "0"s and "1"s are taken from the MNIST dataset.

** Task 2: Random Symbol Equation Dicipherment **
In the earlier task, equations are created using images from the MNIST Images. While in this task, equations were constructed from randomly selected characters sets of the Omniglot dataset, i.e, a random Omniglot symbol is used to represent '1', '0', '+', '=' each.

We use a CNN as the Machine Learning model for these tasks.
