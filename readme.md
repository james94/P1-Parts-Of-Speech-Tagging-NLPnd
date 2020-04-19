# Part of Speech Tagging

**Part of Speech Tagging (POS)** is the process of determining the syntactic category of a word from the words in its surrounding context.

## Table of Contents

- Introduction
- Hidden Markov Model Architecture
- Requirements
- Getting Started
- Resources

## Introduction

Part of Speech Tagging can be used for many Natural Language Processing (NLP) tasks like determining pronounciation during speech synthesis, for information retrieval and for word sense disambiguation. In the project, Part of Speech Tagging was used to tag the words in sentences with their corresponding part of speech: `., ADJ, ADP, ADV, CONJ, DET, NOUN, NUM, PRON, PRT, VERB, X`, which is defined in **[tags-universal.txt](tags-universal.txt)** file. The parts of speech can also be thought of as labels. In the project notebook, the [Pomegranate](https://github.com/jmschrei/pomegranate) library was used to develop a hidden Markov model to help label these words with their corresponding part of speech based on the existing labeled data in the text file coming from a [universal tagset](http://www.petrovi.de/data/universal.pdf).

Hidden Markov models have been able to achieve >96% tag accuracy with larger tagsets on realistic text corpora. Text corpora is a large and structured set of texts. Hidden Markov models have also been used for speech recognition and speech generation, machine translation, gene recognition for bioinformatics, and human gesture recognition for computer vision, and more.

## Hidden Markov Model Architecture

For simplicity, I will describe the Hidden Markov Model Architecture using 3 parts of speech: `NOUN, MODAL VERB, VERB`. So when we have a sentence "Jane will see," we tag it with the parts of speech in which "Jane" is the "NOUN", "will" is the "MODAL VERB" and "see" is the "VERB". 

To teach the computer how to tag parts of speech within a sentence, first we do some data processing on the text corpora defined in **[brown-universal.txt](brown-universal.txt)** to create a tag emission probabilities discrete distribution for each Hidden Markov Model state as shown in **Figure 1**. Next we calculate the transition probabilities from start state to each tag, between every pair of tags and from each tag to the end state as shown in **Figure 1**. 

![hidden-markov-model-10](docs/images/hidden-markov-model-10.jpg)

**Figure 1**: Hidden Markov Model Emission and Transition Probabilities [1]

To calculate the tag emission probabilities, we divide each word count for a particular tag by that particular tag count. For example, the word "Mary" appeared 4 times as a "NOUN", the "NOUN" count for the all the words is 9 by adding all the word counts in the numerators. So, the emission probability for the "NOUN" to be the word "Mary" is 4/9 as shown in **Figure 2**. Once this procedure is done for all emission probabilities, they are passed into the discrete distribution for each Hidden Markov Model state. Each state has a tag and emission probabilities to words as shown in **Figure 2**.

![hidden-markov-model-5](docs/images/hidden-markov-model-5.jpg)

**Figure 2**: Hidden Markov Model Emission Probabilities [1]

To calculate the transition probabilities from the start state to each tag, we divide each starting tag count by the sum of all starting tag counts. As we do this procedure for each transition probability, each probability is added as a model transition for the start state to each tag **Figure 3**. Likewise, to calculate the transition probabilities from each tag to the end state, we divide each ending tag count by the sum of all ending tag counts. Then each probability from each tag to the end state is added to the model transition **Figure 3**. To compute the transition probabilities between every pair of tags, we divide each bigram count by the unigram tag count. Then each probability between every pair of tags is added to the model transition as shown in **Figure 3**. A bigram is a pair of tags. A unigram is the tag.

![hidden-markov-model-8](docs/images/hidden-markov-model-8.jpg)

**Figure 3**: Hidden Markov Model Transition Probabilities [1]

## Requirements

- git
- anaconda or miniconda
- Note: Tested on Windows 10 with Anaconda

## Getting Started

0. (Optional) The provided code includes a function for drawing the network graph that depends on [GraphViz](http://www.graphviz.org/). You must manually install the GraphViz executable for your OS before the steps below or the drawing function will not work.

1. Open a terminal and clone the project repository:

~~~bash
$ git clone https://github.com/james94/P1-Parts-Of-Speech-Tagging-NLPnd
~~~

2. Switch to the project folder and create a conda environment (note: you must already have Anaconda installed):

~~~bash
$ cd hmm-tagger
hmm-tagger/ $ conda env create -f hmm-tagger.yaml
~~~

3. Activate the conda environment, then run the jupyter notebook server. (Note: windows users should run `activate hmm-tagger`)

~~~bash
hmm-tagger/ $ source activate hmm-tagger
(hmm-tagger) hmm-tagger/ $ jupyter notebook
~~~

Depending on your system settings, Jupyter will either open a browser window, or the terminal will print a URL with a security token. If the terminal prints a URL, simply copy the URL and paste it into a browser window to load the Jupyter browser. Once you load the Jupyter browser, select the project notebook (HMM tagger.ipynb) and follow the instructions inside to complete the project.

### References

[1] [Udacity NLP Nanodegree: Lesson 7 - Part of Speech Tagging with HMMs](https://www.udacity.com/course/natural-language-processing-nanodegree--nd892)

[2] [Pomegranate: Hidden Markov Models](https://pomegranate.readthedocs.io/en/latest/HiddenMarkovModel.html)

[3] [soheillll: Hidden Markov Model Part of Speech tagger](https://github.com/soheillll/Hidden-Markov-Model-POS)