+++
title = 'Sentiment Analysis: Part 1'
date = 2024-09-03T11:10:04-07:00
draft = false
tags = ['NLP', 'Sentiment Analysis']
keywords = ['NLP', 'Sentiment Analysis']
ShowToc = true
+++

### The Goal

The goal is to learn about **Sentiment Analysis** and how to perform it. As part of the fellowship.ai challenge, I want to write down what I have learnt through this process and what I can do to further learn more. The prompt in the challenge is really vague, with just a link to the IMDB Dataset that contains 50k movie reviews and that I should perform Sentiment Analysis on it.

### Current State Of The Art (September 2024)

![Figure 1: Current SoTA](sota.png#center "Figure 1: Current SoTA")

^Data pulled from NLP Progress.^

^\* Side note, NLP Progress is amazing but why don't we have something equivalent for other areas of deep learning? Say Computer Vision?^

### What is Sentiment Analysis?

Sentiment Analysis is the task of classifying the polarity of given text.

I have, in the past, at a hackathon with some friends, scraped public data from Reddit and Twitter that contains mentions of publicly traded companies and performed sentiment analysis (through the Google API at the time) on them. We used that data and corroborated with how the stock performed that day on the markets to signal whether or not the stock is a buy or a sell that day.

### The Strategy

I think I would like to start with how sentiment analysis has evolved throughout the years. And I would also like to compare and contrast the different start of the art models and learn how they work

_The dataset that I will be using would be the IMDB dataset. It contains 50k reviews and are equally split between positive and negative ones. Negative review scores are <= 4 and positive reviews are >= 7. No more than 30 reviews are included per movie._

### Throughout the years

For simplicity, I have asked ChatGPT to summarize the improvements in sentiment analysis throughout the decades.

- **2013-2014**: Traditional ML models like Naive Bayes and SVM, with lexicon-based methods, dominated sentiment analysis.
- **2015-2016**: Word2Vec and GloVe embeddings, along with early (Recurrent Neural Networks) RNNs and (Long Short-Term Memory) LSTMs, improved sentiment analysis by capturing semantic relationships.
- **2017-2018**: Attention mechanisms, ELMo, and ULMFiT introduced better context handling and transfer learning to sentiment analysis.
- **2019-2020**: BERT and Transformer models revolutionized sentiment analysis with bidirectional context understanding and fine-tuning.
- **2021-2022**: GPT-3 and multilingual models like XLM-R enabled few-shot and zero-shot learning in sentiment analysis.
- **2023-Present**: Sentiment analysis reached human-level accuracy with models like GPT-3 excelling in few-shot, zero-shot learning, and multimodal data analysis.

#### What are Recurrent Neural Networks?

I think this article assumes that we know what recurrent neural networks are. I think a pretty good learning resource for this is Ava and Alexander Amini's lecture series on YouTube. While I think the lecture on recurrent neural network itself wasn't the best out of the lecture series, it gave me a good idea on what it is. In fact, nearly all the graphics in this article are pulled from their lecture series.

The way that I think about Recurrent Neural Networks is that it is a regular feed forward neural network, but with the addition of the time parameter. It is used for sequential data, aka, speech, language, time serieses.

To do that, it loops on itself, aka, recurrence. It has a bunch of states for each step in the sequence that are hidden.

![alt text](rnn.png#center)

##### Challenges of the Recurrent Neural Network

Exploding Gradient Problem

#### What are Long Short-Term Memory?

1. Maintain a cell state
2. Use gates to control the flow of information

- forget gate gets ride of irrelevant information
- store relevant information from current input
- selectively update cell state
- output gate returns a filtered version of the cell state

3. Backpropagation through time with partially uninterrupted gradient flow

#### What are Word Embeddings?

For RNNs, to adapt them for usage in natural language, we need to have a way to represent words in the form that a neural network would understand. Word embeddings are one way of doing them in a way that captures semantic relationships between words. 

For example: 
```
{
    "dog": 1
    "cat": 2
    "apple": 30 -> since apple is rarely used with dog or cat
}
```

- Word2Vec
- GloVe

#### What are Attention Mechanisms?

Recurrence is expensive. To solve it, we only take into consideration what is deserving of our attention.

1. Identify which parts to attend to
2. Extract the features with high attention

Goal: Identify and attend to most important features in input

1. Encode position information
2. Extract query, key, value for search
3. Compute attention weighting
   - Take the query and key vectors, and compute pairwise similarity (using cosine similarity)
4. Extract features with high attention
   ( Andrej Kaparthy makemore )

![alt text](attention-mechanism.png#center)

CoVe (Context Vectors)
 - Originally trained for machine translating tasks
 - Contextualizled word embeddings that are pre-trained on machine translation 

ElMo (Embeddings from Language Models)
- Contextualized Word Embeddings
- bidirectional LSTM Network to create word embeddings
- Transfer Learning 
ULMFiT

#### What are Transformers

Recurrent neural network that is built on attention. It is essentially, multiple attention mechanisms that are put together

BERT
BERT is a transformer-based model pre-trained on large corpora and then fine-tuned for specific tasks like sentiment analysis. It uses a bidirectional approach to understand context, significantly improving sentiment classification.

GPT

#### What is few-shot and zero-shot learning?
