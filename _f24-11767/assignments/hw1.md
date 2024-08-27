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

hwtitle: "HW 1: Crowdsourced Annotations"

---

<hr>

**HW 1: Crowdsourced Annotations**
====

- **Due 11:59pm, Tuesday 2/15.**
- Zip the code and a PDF write-up into a single tar/zip file and submit through Canvas. Code will not be graded.

Goals
====
Crowdsourcing annotations has become a fundamental aspect of NLP research. The goal of this assignment is to explore the ethical implications of soliciting crowdsourced data, specifically social biases that may emerge when asking for generated sentences.

Overview
====
In this homework, you will perform a “bias audit” of an NLP dataset produced by crowdsourcing. You will attempt to measure the presence of social stereotypes in this dataset that may have harmful effects if used to train classifiers in downstream tasks.

You will use pointwise mutual information (PMI) to find which associations are being made with identity labels. PMI can be used as a measure of word association in a corpus, i.e. how frequently two words co-occur above what might just be expected based on their frequencies. See the [PMI Wikipedia page](https://en.wikipedia.org/wiki/Pointwise_mutual_information) for more details. Here we use PMI to measure which words co-occur with labels for identities. This allows us to see associations that may perpetuate stereotypes.

After this analysis, you will present specific examples from the data that you speculate could be particularly biased and problematic. In the optional advanced analysis, you will expand this analysis to another corpus.

Data and Resources
====
- [SNLI corpus](https://nlp.stanford.edu/projects/snli/snli_1.0.zip), a popular dataset for the NLP task of natural language inference. You can read more about the dataset and task on the [SNLI website](https://nlp.stanford.edu/projects/snli/) or in the original paper ([Bowman et al. 2015](https://aclanthology.org/D15-1075/)).
    - Use the training data CSV or JSON lines file (`snli_1.0_train.jsonl`) in the SNLI corpus. The `sentence1` column with premise that was supplied to annotators, and the `sentence2` column is the hypotheses that annotators came up with. See other details about the corpus format in the README supplied with SNLI.
- [List of identity labels](/teaching/11-830/assignments/files/identity_labels.txt) (based on [Rudinger et al. 2017](https://aclanthology.org/W17-1609/)).

Basic Requirements
====
Completing the basic requirements will earn a passing (B-range) grade.

**Word association analysis:** First, build a tool for calculating pointwise mutual information (PMI) between unigram frequencies in the SNLI dataset. Your tool should take a unigram, with word frequencies relative to a corpus, as input and give a list of other unigrams in the corpus ranked by PMI. Terms that occur less than 10 times in the corpus should not be considered; optionally you can consider other thresholds. For preprocessing, lowercase, remove stopwords and tokenize the data. Note that there are duplicate premises and hypotheses in the data; remove these and just look at unique utterances.

Here’s how you can calculate PMI. Let $$c(w_i)$$ be the count of word $$w_i$$ in the corpus and $$c(w_i, w_j)$$ be the number of times that $$w_i$$ and $$w_j$$ occur in the same premise or hypothesis. 
If they co-occur more than once within a premise or hypothesis, you can still just calculate that as one. With  $$N$$ as the number of documents (premises or hypotheses) in the corpus, we define $$P(w_i)$$ 
as the word frequency $$c(w_i) / N$$. Then PMI is:

$$PMI(w_i, w_j) = log_2 \frac{p(w_i, w_j)}{P(w_i)P(w_j)} = log_2\frac{N\cdot c(w_i, w_j)}{c(w_i)c(w_j)}$$

Compute PMI between the identity labels in the provided list and all other words in the SNLI training corpus (see details in the Data and Resources section above. Look at the top associated words for identity labels of your choice. Do you see any that may reflect social stereotypes? It is helpful to compare the top PMI words for certain identity terms with other related ones (such as *men* compared with *women*). Note that some terms in the list do not occur in the data; they are included for advanced analysis on possible other corpora.

Calculate PMI separately for identity terms in the premises, which are the original provided captions from the Flickr30k image captioning dataset, and identity terms in the hypotheses, which were elicited in a crowdworking task. You will compare the associations made in the write-up.

**Qualitative analysis:** Find specific hypotheses from the dataset where an identity label occurs with a top-associated term that shows some social bias or does not. Look at 1-2 examples for at least 5 different identity labels. Also note the label (entailment, contradiction, neutral) and consider the impact of asking annotators for certain types of inference.

**Crowdsourcing set-up:** Read about what crowdworkers were asked to do in constructing the SNLI corpus in the SNLI paper. Come up with at least one idea about how the designers of the crowdsourcing task might have mitigated any social bias you found in your analysis. For example, are there certain topics that often led to biased hypotheses? Could the task have been structured differently or different instructions given to mitigate bias?

Advanced Analysis
====
Choose one of the options below for advanced analysis.

New corpus
----
Choose another crowdsourced NLP or ML dataset and perform a similar bias audit based on identity terms. Datasets to consider include (but are not limited to!):

- [MNLI](https://cims.nyu.edu/~sbowman/multinli/): The Multi-Genre Natural Language Inference (MultiNLI) corpus is a crowd-sourced collection of 433k sentence pairs annotated with textual entailment information. The corpus is modeled on the SNLI corpus, but differs in that covers a range of genres of spoken and written text, and supports a distinctive cross-genre generalization evaluation. [[download]](https://cims.nyu.edu/~sbowman/multinli/multinli_1.0.zip)
- [ROCStories](https://www.cs.rochester.edu/nlp/rocstories/): 'Story Cloze Test' is a new commonsense reasoning framework for evaluating story understanding, story generation, and script learning. This test requires a system to choose the correct ending to a four-sentence story. To enable the Story Cloze Test, we created a new corpus of five-sentence commonsense stories, 'ROCStories'. This corpus is unique in two ways: (1) it captures a rich set of causal and temporal commonsense relations between daily events, and (2) it is a high quality collection of everyday life stories that can also be used for story generation. [[download of original 2016 corpus]](/teaching/11-830/assignments/files/rocstories_spring2016.csv)
- [SQuAD 2.0](https://aclanthology.org/P18-2124/) combines the 100,000 questions in SQuAD1.1 with over 50,000 unanswerable questions written adversarially by crowdworkers to look similar to answerable ones. To do well on SQuAD2.0, systems must not only answer questions when possible, but also determine when no answer is supported by the paragraph and abstain from answering. [[data]](https://rajpurkar.github.io/SQuAD-explorer/)
- [DROP (QA)](https://aclanthology.org/N19-1246/) is a QA dataset which tests comprehensive understanding of paragraphs. In this crowdsourced, adversarially-created, 96k question-answering benchmark, a system must resolve multiple references in a question, map them onto a paragraph, and perform discrete operations over them (such as addition, counting, or sorting). [[data]](https://allennlp.org/drop)

Modify the identity list by adding and/or dropping labels that do or do not occur above a frequency threshold in this new dataset and run the PMI word association analysis. Similar to the basic requirements, discuss stereotypes found in this corpus and give specific examples. Are there differences in the type or degree of stereotypes found compared with the SNLI corpus? Read about the annotation procedure for these datasets. How might these crowdsource tasks have set themselves up --- or not --- for responses that reflect stereotypes in ways that are similar or different from SNLI? Discuss potential implications for new crowdsourced data collection in the write-up.

Phrases
----
Expand the PMI analysis to higher-order n-grams and possibly syntactic phrases. Note that you will want to also expand the identity list to possibly include combinations of identity types (such as *asian man*). Refer to [Rudinger et al. (2017)](https://aclanthology.org/W17-1609/) for ideas here.

Bias with respect to class labels
----
In this assignment you implemented an approach for identifying associations between unigrams and identity labels in a corpus. You can similarly investigate whether identity words (and closely related words via e.g. embedding similarity) have some correlation with *class labels* in text classification tasks, such as [sentiment analysis](https://nlp.stanford.edu/sentiment/index.html). Discuss your results. What are possible implications of such bias for downstream uses of such a classifier? Are there certain model designs that might be more susceptible to such correlations than others?

Association measures
----
Perhaps PMI is not the best lexical association measure to see social bias with identity terms. Explore lexical association measures other than PMI; see [Pecina (2010)](https://link.springer.com/article/10.1007/s10579-009-9101-4) for ideas.

Latest methods
----
Find and implement a recent approach for identifying biases in datasets. Summarize the approach in a couple paragraphs, and how you applied it to SNLI or another dataset. Compare the results to your analysis based on PMI. What are trade-offs of each approach, in terms of implementation, efficiency, results? 

Write-up
====
Each student should submit their own 2-3 page report ([ACL format](https://www.overleaf.com/latex/templates/acl-rolling-review-template/jxbhdzhmcpdm)). Please do not submit more than 4 pages, though you can put large tables and figures in an appendix beyond that if necessary. The report should include:
- The top 5 terms associated with 10 identity labels of your choice by PMI for both premises and hypotheses in the SNLI dataset (variations on the same lemma such as man and men count separately). These terms can indicate social biases you see or not.
- A discussion of associations made in the SNLI dataset that are stereotypical, or a lack thereof. If you see any, discuss differences between premises and hypotheses regarding these stereotypes. Give specific examples of data where these associations are being made, and what potential harm that reinforcing this stereotype in a natural language inference dataset may have.
- A brief discussion of what steps may be taken to mitigate this effect when using crowdsourcing to create and annotate NLP datasets. For example, what instructions could be given to crowdworkers, and more importantly, how might a crowdsource task be structured to elicit fewer stereotypes? Do you think asking for free-form generated sentences from crowdworkers will always produce responses that reproduce stereotypes, or are there ways to give context that may lessen that effect? How much of any bias that you see is due to the original premises provided to annotators?
- [If doing advanced analysis] Results and discussion of advanced analysis.

Grading (100 points)
====
- 20 points: Submitting assignment
- 40 points: Completing basic requirements
- 20 points: Write up is well-written, presents meaningful analysis, and contains all requested information
- 20 points: Advanced analysis

References
====
- Rachel Rudinger, Chandler May, & Benjamin Van Durme. (2017). [Social Bias in Elicited Natural Language Inferences](https://aclanthology.org/W17-1609/). *Proceedings of the First ACL Workshop on Ethics in Natural Language Processing*, 74–79.
- Mor Geva, Yoav Goldberg, Jonathan Berant. (2019). [Are We Modeling the Task or the Annotator? An Investigation of Annotator Bias in Natural Language Understanding Datasets](https://anthology.aclweb.org/D19-1107/). *Proceedings of EMNLP-IJCNLP*.
- Samantha Jaroszewski, Danielle Lottridge, Oliver L. Haimson, Katie Quehl. (2018). [Genderfluid or Attack Helicopter: Responsible HCI Research Practice with Non-binary Gender Variation in Online Communities](https://dl.acm.org/doi/10.1145/3173574.3173881). *Proceedings of the 2018 CHI Conference on Human Factors in Computing Systems*. [link]
- Pavel Pecina. (2010). [Lexical association measures and collocation extraction](https://link.springer.com/article/10.1007/s10579-009-9101-4). *Language Resources & Evaluation* 44:137–158.
- Florian Alexander Schmidt. (2013). [The good, the bad and the ugly: Why crowdsourcing needs ethics](https://ieeexplore.ieee.org/abstract/document/6686081). *Conference on Cloud and Green Computing* (CGC).
- Fabian L. Wauthier, Michael I. Jordan. (2011). [Bayesian bias mitigation for crowdsourcing](https://papers.nips.cc/paper/2011/hash/0768281a05da9f27df178b5c39a51263-Abstract.html). *Advances in Neural Information Processing Systems*.
