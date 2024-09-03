+++
title = 'Sentiment Analysis'
date = 2024-09-03T11:10:04-07:00
draft = false
tags = ['nlp']
keywords = ['nlp']
ShowToc = true
+++

### The Goal

The goal is to learn about Sentiment Analysis and how to perform it. As part of the fellowship.ai challenge, I want to write down what I have learnt through this process and what I can do to further learn more. The prompt in the challenge is really vague, with just a link to the IMDB Dataset that contains 50k movie reviews and that I should perform Sentiment Analysis on it.

### Current State Of The Art (September 2024)

^Data pulled from NLP Progress.^

^\* Side note, NLP Progress is amazing but why don't we have something equivalent for other areas of deep learning?^

![Figure 1: Current SoTA](images/image.png#center "Figure 1: Current SoTA")

### What is Sentiment Analysis?

Sentiment Analysis is the task of classifying the polarity of given text.

I have, in the past, at a hackathon with some friends, scraped public data from Reddit and Twitter that contains mentions of publicly traded companies and performed sentiment analysis (through the Google API at the time) on them. We used that data and corroborated with how the stock performed that day on the markets to signal whether or not the stock is a buy or a sell that day.

### The Strategy

In this article, I want to compare and contrast different models and how they work.

The dataset that I will be using would be the IMDB dataset. It contains 50k reviews and are equally split between positive and negative ones. Negative review scores are <= 4 and positive reviews are >= 7. No more than 30 reviews are included per movie.

I will be reading through the state of the art papers for sentiment analysis.
