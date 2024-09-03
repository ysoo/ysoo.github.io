+++
title = 'Sentiment Analysis: Part 1'
date = 2024-09-03T11:10:04-07:00
draft = false
tags = ['NLP']
keywords = ['NLP']
ShowToc = true
+++

### The Goal

The goal is to learn about **Sentiment Analysis** and how to perform it. As part of the fellowship.ai challenge, I want to write down what I have learnt through this process and what I can do to further learn more. The prompt in the challenge is really vague, with just a link to the IMDB Dataset that contains 50k movie reviews and that I should perform Sentiment Analysis on it.

### Current State Of The Art (September 2024)

![Figure 1: Current SoTA](images/image.png#center "Figure 1: Current SoTA")

^Data pulled from NLP Progress.^

^\* Side note, NLP Progress is amazing but why don't we have something equivalent for other areas of deep learning?^

### What is Sentiment Analysis?

Sentiment Analysis is the task of classifying the polarity of given text.

I have, in the past, at a hackathon with some friends, scraped public data from Reddit and Twitter that contains mentions of publicly traded companies and performed sentiment analysis (through the Google API at the time) on them. We used that data and corroborated with how the stock performed that day on the markets to signal whether or not the stock is a buy or a sell that day.

### The Strategy

I think I would like to start with how sentiment analysis has evolved throughout the years. And I would also like to compare and contrast the different start of the art models and learn how they work

The dataset that I will be using would be the IMDB dataset. It contains 50k reviews and are equally split between positive and negative ones. Negative review scores are <= 4 and positive reviews are >= 7. No more than 30 reviews are included per movie.

### Throughout the years

For simplicity, I have asked ChatGPT to summarize the improvements in sentiment analysis throughout the decades.

- **2013-2014**: Traditional ML models like Naive Bayes and SVM, with lexicon-based methods, dominated sentiment analysis.
- **2015-2016**: Word2Vec and GloVe embeddings, along with early RNNs and LSTMs, improved sentiment analysis by capturing semantic relationships.
- **2017-2018**: Attention mechanisms, ELMo, and ULMFiT introduced better context handling and transfer learning to sentiment analysis.
- **2019-2020**: BERT and Transformer models revolutionized sentiment analysis with bidirectional context understanding and fine-tuning.
- **2021-2022**: GPT-3 and multilingual models like XLM-R enabled few-shot and zero-shot learning in sentiment analysis.
- **2023-Present**: Sentiment analysis reached human-level accuracy with models like GPT-3 excelling in few-shot, zero-shot learning, and multimodal data analysis.
