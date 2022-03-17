---
layout: class
description: Description
importance: 3

# todo: grab this automatically from class?
class_link: /teaching/11-830/
title: "11-830: Computational Ethics for NLP"
semester: Spring 2022
time: 10:10-11:30 Tuesdays & Thursdays
place: Singleton Room, Roberts Engineering Hall <a href="/assets/pdf/Campus-Map-to-Singleton.pdf">[PDF map]</a>
zoom: See <a href="https://canvas.cmu.edu/courses/28069">Canvas</a> or <a href="http://11830workspace.slack.com">Slack</a> for Zoom link.

hwtitle: "HW 3: Privacy and Obfuscation"

---

<hr>

**HW 3: Privacy and Obfuscation**
====

- **Due 11:59pm, Thursday 3/31.**
- **Submission:** Submit a zip/tar file to Canvas. Include your write-up (titled `FirstName_LastName_hw3.pdf`) and a folder containing your code. Code will not be graded.

* * *

## Goals

Online data has become an essential source of training data for natural language processing and machine learning tools; however, the use of this type of data has raised concerns about privacy. Furthermore, the detection of demographic characteristics is a common component of microtargeting. In this assignment, you will explore how to obfuscate demographic traits, specifically gender. The primary goals are (1) develop a method for obfuscating an author's gender and (2) explore the trade-off between obfuscating an author's identity and preserving useful information in the data

* * *

## Overview

The data for this assignment is available [here](/teaching/11-830/assignments/files/assign3_data.tar.gz). Your primary dataset consists of posts from Reddit. Each post is annotated with the gender of the post's author (`op_gender`) and the subreddit where the post was made (`subreddit`). The main text of the post is in the column `post_text`. The contents of the provided data include:

* `classify.py`: a classifier that predicts the author's gender and the subreddit for a post (example run: `python classify.py --test_file dataset.csv`). Note that this file also uses the two provided pickle files.
* `dataset.csv`: your primary data.
* `background.csv`: additional Reddit posts that you may optionally use for training an obfuscation model. A larger version is available [here](https://drive.google.com/file/d/1lVh5B7d35egOnbWi4ilRh1rScuU1Zbdb/view).
* `female.txt`: a list of words commonly used by women.
* `male.txt`: a list of words commonly used by men.

The provided classifier achieves an accuracy of 64.95% at identifying the gender of the poster and an accuracy of 85.85% at identifying a post's subreddit when tested over dataset.csv. Your goal in this assignment is to obfuscate the data in dataset.csv so that the provided classifier is unable to determine the gender of authors, while still being able to determine the subreddit of the post. Note that in this set-up, we treat the provided classifier as a blackbox adversary (please do not try to hack it). This assignment was largely inspired by the paper *Obfuscating Gender in Social Media Writing* ([Knight & Reddy, 2016](https://aclanthology.org/W16-5603/)), which may be a useful reference. Scenerios where this obfuscation model might be useful could be social media users who want to preserve their privacy by hiding their gender from the adversary, without losing the meaning of their post. You could also imagine this is a dataset of health records or other sensitive information that needs to be anonymized before providing it to NLP researchers.

* * *

## Basic Requirements

Completing the basic requirements will earn a passing (B-range) grade

**First**, build a baseline obfuscation model:

* For each post in `dataset.csv`, if the post was written by a man (`M`) and it contains words from `male.txt`, replace these words with a random word from `female.txt`.
* Obfuscate posts written by women (`W`) in the same way (i.e. by replacing words from `female.txt` with random words from `male.txt`)
* Test `classify.py` on your obfuscated data and analyze the results.

**Second**, improve your obfuscation model:

* Instead of replacing words from `male.txt` with randomly chosen words from `female.txt`, choose a semantically similar word from `female.txt` (use the same metric for replacing words from `female.txt` with words from `male.txt`). You may use any metric you choose for identifying semantically similar words. We recommend using cosine distance between pre-trained word embeddings (available [here](http://mccormickml.com/2016/04/12/googles-pretrained-word2vec-model-in-python/)). You can also use SpaCy-based similarity [here](https://spacy.io/usage/linguistic-features) ([example 1](https://ashutoshtripathi.com/2020/09/04/word2vec-and-semantic-similarity-using-spacy-nlp-spacy-series-part-7/), [example 2](https://www.geeksforgeeks.org/python-word-similarity-using-spacy/)).
* Test `classify.py` on data obfuscated using your improved model and analyze the results. The classifier should perform close to random at identifying gender (e.g. <53.5%) and should obtain at least 79% accuracy on classifying the subreddit. 

**Third**, experiment with some basic modifications to your obfuscation models. For example, what if you randomly decide whether or not to replace words instead of replacing every lexicon word? What if you only replace words that have semantically similar enough counterparts?

## Advanced Analysis

Develop your own obfuscation model. We provide `background.csv`, a large data set of Reddit posts tagged with gender and subreddit information that you may use to train your obfuscation model. A larger version of the background corpus is available [here](https://drive.google.com/file/d/1lVh5B7d35egOnbWi4ilRh1rScuU1Zbdb/view). Your ultimate goal should be to obfuscate text so that the classifier is unable to determine the gender of an author (no better than random guessing) without compromising the accuracy of the subreddit classification task. However, creative or thorough approaches will receive full credit, even if they do not significantly improve results. Some ideas you may consider:

* Develop your own lexicons using [pointwise mutual information scores](https://en.wikipedia.org/wiki/Pointwise_mutual_information) or [log odds with a dirichlet prior](https://firstmonday.org/ojs/index.php/fm/article/view/4944/3863).
* Follow the procedure described in ["Obfuscating Gender in Social Media Writing"](https://aclanthology.org/W16-5603/).
* Use an adversarial objective as described in ["Predicting Sales from the Language of Product Descriptions"](https://www-nlp.stanford.edu/pubs/pryzant2017sigir.pdf) to train a model that is good at predicting subreddit classification but bad a predicting gender. The key idea in this approach is to design a model that does not encode information about protected attributes (in this case, gender).
* Use a model for style transfer to generate the text, such ["Style Transfer Through Back-Translation"](https://arxiv.org/abs/1804.09000).

In your report, include a description of your model and results.

* * *

## Write-up

Write a 2-3 page report (ACL format) `FirstName_LastName_hw3.pdf`. Please do not write more than 4 pages. The report should include:

* Description of baseline, improved and advanced (if completed) obfuscated models.
* Description of the experiments you tried with your improved obfuscation model.
* Results for your models by using them to obfuscate `dataset.csv` and running `classify.py` over your obfuscated test data. 
* Qualitative examples of text obfuscated with your models.
* A brief discussion of the ethical implications of obfuscation and privacy that draws from concepts covered during lecture.

* * *

## Grading (100 points)

* 20 points - Submitting assignment.
* 40 points - Completing basic requirements.
* 20 points - Write up is well-written, presents meaningful analysis, and contains all requested information.
* 20 points - Advanced analysis.