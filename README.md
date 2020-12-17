
# A very spooky lightning talk :jack_o_lantern:

## Overview

The goal of this proect was to experiment with emerging language models in a way that celebrates the best holiday season (Halloween!). I trained the OpenAI's GPT-2 model on Reddit creepy stories, with the goal of generating new stories! I implemented [the model](https://colab.research.google.com/drive/1K471UPqVbNQjRLlYoJCNElRPcsb61uia) in Google Colab. I presented the results of this project in an October 2019 [Women Who Code DC Lightning Talk](https://docs.google.com/presentation/d/e/2PACX-1vTEMALPHw-yQRXVnJBP_nj0yeqW60jLnGLIRgdfDziqJzcX7SiSUbbx1jLaGSeWqeFjkIG7odo3wuyj/pub?start=false&loop=false&delayms=3000). This repository stores the data outputted by the GPT model and the cleaning script used to preprocess the text data.

## Motivation

I really enjoy natural language processing, and I wanted to explore bleeding-edge text generation methods. Luckily for me, in September 2019 OpenAI had just released its GPT-2 model, at the time the best-in-class large language model. I also encountered a Python wrapper to GPT-2 as well as an easy platform to train the model (Google Colab). A little external pressure (completing the project in time to present the results at a Halloween-themed tech meetup) was the last bit of motivation I needed to start exploring this tool.

## How I completed this project

### Data cleaning

The data I used for this project came from Google's BigQuery Public Datasets. I considered using the praw package in Python to pull posts, but GET requests are capped and the process of pulling the data would have taken many days. I pulled all posts in the creepypasta subreddit posted from September 2015 - September 2019; the query is [here](https://console.cloud.google.com/bigquery?sq=411015426768:72919a8f196944f6a32b0da1ca5e7050). 

In the Jupyter notebook [Reddit posts cleaning.ipynb](https://github.com/alliesaizan/spooky-lightning-talk/blob/master/Reddit%20posts%20cleaning.ipynb), I preprocess the raw subreddit data. I remove rows with where the post text is missing and word tokenize the data to enable data exploration. Looking through the data, I discovered numerous instances of short posts that were plugs for other content; to remove this data, I kept only posts with more than 250 words. I was limited in the size of data I could upload to Google Drive, so I took a random sample of 8,000 posts to cap the file size. I then saved the pipe-delimited data to Google Drive for ingestion into the GPT-2 model.

### GPT-2

I leveraged the [GPT-2 model](https://colab.research.google.com/drive/1K471UPqVbNQjRLlYoJCNElRPcsb61uia) in a Google Colab notebook using the gpt-simple Python package. gpt-simple is a wrapper for the GPT-2 module that enables text generation. The Colab notebook was developed by Max Woolf, and the only edits I made were to upload my data and tune the temperature parameter of the generate() method. The temperature parameter alters the randomness of the generated results. The model took a few hours to fully train. I exported the generated text to the file *gpt2_gentext_20191006.txt*.

## Findings

I found that GPT-2 was surprisingly good at replicating narrative structures and conversations. However, it did a poor job of replicating scares. The GPT-2 generated stories were mostly all set-up and no thrills. Creepypasta stories tend to have lengthy set-up, and I supect the model mistakes this part of the story as being narratively important. The generated stories also tended to repeat words or phrases nonsensically, and this problem was worse with higher values of the temperature parameter. I did get some pretty funny outcomes though, including one story with "I'm sorry" repeated over and over.
