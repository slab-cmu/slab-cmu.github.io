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

hwtitle: "HW 2: Civility in Communication"

---

<hr>

**HW 2: Civility in Communication**
====

- **Due 11:59pm, Thursday 3/17.**
- Submission: Submit your assignment through Canvas. Include 3-4 separate files in a zipped into zip/tar file: your write-up (titled `FirstName_LastName_hw2.pdf`), your predictions over `test.tsv` titled `FirstName_LastName_test.tsv`, your improved predictions over `test.tsv` titled `FirstName_LastName_advanced.tsv` (if completed), and your code. Code will not be graded.

* * *

## Goals

As we have discussed in class, abusive language on online platforms has become a major concern in the past few years. However, developing automated methods for flagging and censoring abusive language has proved to be difficult and prone to unwanted biases. The goals of this assignment are to (1) explore the challenges and ethical issues behind developing classifier for identifying offensive language (2) develop techincal solutions that aim to address these challenges.

* * *

## Overview

In this assignment, you will explore an off-the-shelf toxicity classifier as well as build your own models. In general, you will evaluate models using two criteria: (1) performance over hate speech detection (Accuracy and F1 Score where “NOT” is considered the positive label) and (2) False Positive Rate (FPR), how often the model misclassifiers non-toxic speech as toxic, specifically for comments associated with different demographic dialects. Poor performance over hate speech classification suggests that the model is not accurate enough to be useful, while poor or imbalanced FPR indicates that the model may impose racial biases.

The primary data for this assignment is available [here](/teaching/11-830/assignments/files/civility_data.tar.gz) . **Please note that the data contains offensive or sensitive content, including profanity and racial slurs.**

We provide data drawn from two sources. The first (files `train.tsv` and `dev.tsv`) consists of tweets annotated for offensiveness taken from the [2019 SemEval task](https://competitions.codalab.org/competitions/20011) on offensive language detection. In the files `train.tsv` and `dev.tsv`, the first column (`text`) contains the text of a tweet, the second column (`label`) contains an offensiveness label:

*   (NOT) Not Offensive - This post does not contain offense or profanity.
*   (OFF) Offensive - This post contains offensive language or a targeted (veiled or direct) offense

The file `offenseval-annotation.txt` provides additional details on the annotation scheme.

We additionally provide a data set of tweets proxy-labelled for race in the file titled `mini_demographic_dev.tsv`. This data is taken from the [TwitterAAE](http://slanglab.cs.umass.edu/TwitterAAE/) data set and uses posterior proportions of demographic topics as a proxy for racial dialect ([details](https://www.aclweb.org/anthology/D16-1120.pdf)). The first column (`text`) contains the text of the tweet, and the second column (`demographic`) contains a label: “AA” (for “African American”), “White”, “Hispanic”, or “Other”. For this assignment, we assume that no tweet in the TwitterAAE data set contains toxic language. Thus, any tweet in this file that is classified as toxic is a false positive.

Finally, both development sets (`dev.tsv` and `mini_demographic_dev.tsv`) contain a column `perspective_score`, which contains a toxicity score. These scores were obtained using the [PerspectiveAPI](https://www.perspectiveapi.com/) tool released by Alphabet. This tool is intended to help “developers and publishers…give realtime feedback to commenters or help moderators do their job.”

In all data sets, user mentions have been replaced with the token `@USER`.

* * *

## Basic Requirements

Completing the basic requirements will earn a passing (B-range) grade

**Off-the-shelf Model Exploration**

*   Use the provided perspecitve_score values to classify each tweet in `dev.tsv` and `mini_demographic_dev.tsv` as toxic or non-toxic. As a starting point, assume that a tweet is considered offensive if it contains a toxicity score > 0.8 (you may optionally explore other thresholds).
*   Using `dev.tsv` report the Accuracy and F1 Scores of PerspectiveAPI for offensiveness classification.
*   Using `mini_demographic_dev.tsv`, separately report the FPR for each demographic group (assuming no tweet in `mini_demographic_dev.tsv` is actually offensive).
*   Briefly discuss your results

**Custom Model Exploration**

*   Build your own classifier to distinguish offensive (OFF) tweets from non-offensive (NOT) tweets. Your model should be trained on `train.tsv` and should obtain an accuracy of at least 70% and an F1 score of at least 80% over `dev.tsv` (this should be easy to obtain with surface-level features).
*   Report the accuracy and F1 score of your model over `dev.tsv`
*   Report FPR over `mini_demographic_dev.tsv`
*   Briefly discuss your results. How does your model compare to PerspectiveAPI?

**Test Set Predictions**

*   The file `test.tsv` contains a mix of data from the the TwitterAAE data set and the 2019 SemEval task. Use your model to make OFF/NOT predictions for the `test.tsv` samples, and place these predictions in a separate file titled FirstName_LastName_test.tsv. Offensiveness labels (OFF/NOT) should be in a column with the heading `label`. Please use tabs (`\t`) to separate columns.

**Write-up**

Submit a 2-3 page report (ACL format) titled `FirstName_LastName_hw2.pdf`. Please do not submit more than 4 pages. The report should include:

*   Results and discussion of your analysis of the PerspectiveAPI scores
*   Description of your offensiveness classifier
*   Results and discussion of your classifier over the dev sets
*   Description of your advanced analysis model and results over dev sets (if completed)
*   A brief (1 paragraph) discussion of the ethical implications of using machine learning to combat abusive language. This discussion should refer to your observations from this assignment as well as refer to issues discussed in class or drawn from additional references. Questions you might consider include:

*   How should we define offensive language?
*   What is the cost of misclassification? Who is negatively impacted by missclassification?
*   What are concerns around collecting and annotating training data?

Be sure to cite all references.

* * *

## Advanced Analysis

Choose one of the two options below for advanced analysis:

**Improve your preliminary classifier**
You may aim to improve accuracy/F1 of hate speech classification, or FPR, or to improve both metrics simultaneously. If you choose to focus on one metric, still report results for the other metric and discuss any trade-offs. Creative model architectures or feature crafting will receive full credit, even if they do not improve results.

In your report, include a description of your model and results over dev.tsv. Additionally, use your improved classifier to predict results over `test.tsv` and place these predictions in a file titled `FirstName_LastName_advanced.tsv`.

In order to facitilate analysis, we provide a larger data set [here](https://drive.google.com/file/d/1CqFfZySymPaU8jJrCP50ouKl2XMaygBr/view?usp=sharing). This extended data set contains full training and dev sets from the TwitterAAE data set, as well as additional data annotated for hate speech drawn from a different paper ([ICWSM, 2017](https://www.aaai.org/ocs/index.php/ICWSM/ICWSM17/paper/viewPaper/15665)). Note that user mentions have not been replaced in this data set. You are free to explore any ideas you have. We provide a few pointers for inspiration.

If you choose to maximize performance over offensiveness classification, you may choose to develop a more sophisiticated model for hate speech detection. Some prior work includes:

*   [A Survey on Hate Speech Detection using Natural Language Processing](http://www.aclweb.org/anthology/W17-1101) (This has references to many other papers)
*   [Detecting Hate Speech on the World Wide Web](http://www.aclweb.org/anthology/W12-2103)
*   [Deep Learning for Hate Speech Detection in Tweet](https://arxiv.org/pdf/1706.00188.pdf)
*   [Hate Speech Detection with Comment Embeddings](http://www.www2015.it/documents/proceedings/companion/p29.pdf)

Models from prior SemEval tasks may also be helpful. Additionally, the provided `train.tsv` file contains annotations for different types of offensive language (e.g. untargeted vs. targeted, labels are in the third column titled `category`), which you may also consider leveraging.

If you choose to improve FPR, you may wish to leverage the provided `demographic_train.tsv` file. Data from this file could be used to balance your training data or to train a model with an adversarial object. Some related work includes:

*   [Predicting Sales from the Language of Product Descriptions](https://www-nlp.stanford.edu/pubs/pryzant2017sigir.pdf)
*   [Topics to Avoid: Demoting Latent Confounds in Text Classification](https://arxiv.org/abs/1909.00453)
*   [Gender Bias in Contextualized Word Embeddings](https://arxiv.org/pdf/1904.03310.pdf)


**Adapt to Gab**
As a second option, you can explore how to adapt your classifier to a different data domain from Twitter and a slightly different task.
[Kennedy et al., 2021](https://psyarxiv.com/hqjxn/) introduces a new annotation scheme for “hate-based rhetoric” including Human Degradation (HD), Calls for Violence (CV), Vulgar/offensive (VO). The Gab Hate Corpus (GHC) annotates posts from the website gab.com for these three categories (among other variables like targeted group/framing). Gab is commonly used by political extremists and the alt-right [Andrews 2021](https://www.washingtonpost.com/technology/2021/01/11/gab-social-network/), so that hate speech is more concentrated than on Twitter with a different distribution over topics/targeted groups. To investigate how well your model can do, you can select one or more of the hate-based rhetoric categories to evaluate on. Then, you can train a new classifier over the Gab training data to compare performance with the preliminary classifier. The Gab Hate Corpus also contains several variables for targeted populations/framing. It would be neat to look more closely at how performance differs over speech targeting different groups (e.g. political identity (POL), racial/ethnic identity (RAE)). Alternatively, you can also develop methods to adapt a model trained on Twitter assuming little or no training data from Gab. Dataset available [here](/teaching/11-830/assignments/files/gab_data.tar.gz).



* * *

## Grading (100 points)

*   20 points - Submitting assignment
*   40 points - Completing basic requirements
*   20 points - Write up is well-written, presents meaningful analysis, and contains all requested information
*   20 points - Advanced analysis
*   Additional points of extra credit will be awarded to students with particularly creative classifiers, meaningful analyses, or high performance over `test.tsv`.

* * *

## Implementation Tips

*   You are welcome to use existing packages. Consider tools like nltk and gensim for text processing and tools like sklearn for constructing baseline classifiers.

* * *

## References

*   The Risk of Racial Bias in Hate Speech Detection. Maarten Sap, Dallas Card, Saadia Gabriel, Yejin Choi, and Noah A. Smith. Proceedings of ACL 2019.
*   Automated hate speech detection and the problem of offensive language. Thomas Davidson, Dana Warmsley, Michael Macy, and Ingmar Weber. Proceedings of ICWSM 2017.
*   Demographic Dialectal Variation in Social Media: A Case Study of African-American English. Su Lin Blodgett, Lisa Green, and Brendan O'Connor. Proceedings of EMNLP 2016.
*   Racial Bias in Hate Speech and Abusive Language Detection Datasets. Thomas Davidson, Debasmita Bhattacharya, and Ingmar Weber. Proceedings of Third Abusive Language Workshop at ACL 2019.
*   SemEval-2019 Task 6: Identifying and Categorizing Offensive Language in Social Media (OffensEval). Marcos Zampieri, Shervin Malmasi, Preslav Nakov, Sara Rosenthal, Noura Farra, and Ritesh Kumar. Proceedings of 13th International Workshop on Semantic Evaluation at NAACL 2019\.
