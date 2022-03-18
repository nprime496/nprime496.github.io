# A True Love Story



## Context (with style)

*In the lovely land of Twitter, two new avatars emerged: MonsieurSow (jan 2016) and Mrs_Excellence (avril 2011). they lived their peaceful life in the unwelcoming world. they engaged in a very poignant relationship on the network, inspiring many and drawing the wrath of others.
It was then that hordes of trolls arose claiming that the idyll of the avatars was purely narcissistic because only one person was hiding behind this duality. Today we are going to try to verify with the means at our disposal and this dear data science the statements of these trolls. Is this a new succulent revelation that the platform is crazy about or the delusions of jealous?*

## Stylometry in a nutshell


Stylometry is the quantitative study of literary style through computational distant reading methods. It is based on the observation that authors tend to write in relatively consistent, recognizable and unique ways. For example:

Each person has their own unique vocabulary, sometimes rich, sometimes limited. Although a larger vocabulary is usually associated with literary quality, this is not always the case. Ernest Hemingway is famous for using a surprisingly small number of different words in his writing,1 which did not prevent him from winning the Nobel Prize for Literature in 1954.
Some people write in short sentences, while others prefer long blocks of text consisting of many clauses.
No two people use semicolons, em-dashes, and other forms of punctuation in the exact same way.

I may have quoted wikipedia. 


We usually use the Burrows’ Delta algorithm, a well-known stylometric technique. The library can also calculate the probability that two books were by the same author.


## Objectives

what we will try to do in the following will be to determine whether or not, in the light of the data science methods at our disposal, we can determine whether the two accounts are managed by the same person.

## Implementation

we will use a library dedicated to stylometry although little known: faststylometry. It allows us to compare authors of texts by their writing style. 

### Data collection

Obviously, since the goal is to be able to distinguish if the accounts are managed by the same person, our starting point will be Twitter.

Thus, thanks to the Twitter API, I was able to retrieve the tweets of the main subjects. However, for cross-validation reasons, several other accounts quite related to the main accounts have been recovered.


| account        | tweets |
|----------------|--------|
| monsieursow    | 1840   |
| mrs_excellence | 2252   |
| bokulakalulu   | 2498   |
| allegrafosh2   | 1701   |
| kanindawinner  | 2855   |
| gkk242         | 3090   |
| leparrainrdc   | 1454   |
| hamouly_       | 3118   |

### Exploratory data analysis


### What's your style

The methodology used was to divide all the tweets from each account into subsets. These subsets were further divided into a training set and a test set.

Thus, we can check if the model is able to recognize texts from the same author and have reference values.

We thus calculate the burrow score of the different authors based on the training and test texts.

| ![](/assets/images/lovestory/burrow_delta.png) |
|:--:|
| <b> probabilities's output matrix</b>|

It may seem incomprehensible but it is simply the burrow's delta score of the test tweets compared to the authors. So for each row we have an author, and each column represents a set of tweets, the value in each cell represents the burrow score value (lower is better).

we can see that the different tweets can be separated are easily differentiated thanks to the burrow score. On the diagonal, we find the lowest values showing that tweets from the same author have the same structure. However, note that the burrow score of MonsieurSow and Mrs_Excellence (our subjects) are strangely low. Almost the same value as Leparrainrdc, let's continue the analysis to decide.

### Are you really original ?

The burrow score is quite difficult to interpret, it would be much easier to have a probability that a text is from an author.

We are going to use a faststylometry feature that allows us to train a model to predict whether a text belongs to an author based on the burrow score.

| ![](/assets/images/lovestory/proba.png) |
|:--:|
| <b> Burrow's delta matrix</b>|



## References

- [Introduction to stylometry with python](https://programminghistorian.org/en/lessons/introduction-to-stylometry-with-python)

- [Fast Stylometry Tutorial](https://freelancedatascientist.net/fast-stylometry-tutorial/)

- [faststylometry](https://github.com/fastdatascience/faststylometry)

- [Stylometry wikipedia](https://en.wikipedia.org/wiki/Stylometry)