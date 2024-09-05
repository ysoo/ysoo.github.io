+++
title = 'Sentiment Analysis: Part 2'
date = 2024-09-03T11:10:04-07:00
draft = true
tags = ['NLP', 'Sentiment Analysis']
keywords = ['NLP', 'Sentiment Analysis']
ShowToc = true
+++

#### From the previous episode

In the previous article in this series, we talked about different models that exists out there for semantic analysis.

#### The math behind everything
In this article, I want to explore more behind the math and parameters that are used in these models. How would we use it for just about everything that involves natural language processing? What do we tweak to make it do what we want it to do? 

Some resources in this series involves Andrej Kaparthy's makemore as well as the 3Blue1Brown series on neural networks. 

### Implementation

In this article, I want to write down the learning journey as I try to implement **BERT** (Bidirectional Encoder Representations from Transformers) on the IMDB movie reviews database.

I will be using PyTorch and a Jupyter Notebook on this journey.
