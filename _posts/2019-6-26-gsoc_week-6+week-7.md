---
title:  "Week 6 + Week 7 (ASR - German)"
date:   2019-7-10
layout: single
author_profile: true
comments: true
tags: [GSoC, ASR]
category: GSoC
toc: true
toc_label: "Contents"
toc_icon: "heart"
---

Link to [Repository of Code](https://github.com/AASHISHAG/asr-german)

### Describe my work briefly

I am happy to update on my Week 6 and Week 7 progress. I am progressing well with the project as per the proposal. I spent this period working on Acoustic Modelling.

### Acoustic models

Acoustic models are the statistical representations of a phoneme’s acoustic information.

The acoustic models are created by training the models on acoustic features from labeled data, i.e. the transcribed speech corpus. Kaldi provides tremendous flexibility and power in training own acoustic models.

In order to train an end-to-end ASR pipeline, we need:

1. Monophone models

A monophone model is an acoustic model that does not include any contextual information about the preceding or following phone. It is used as a building block for the triphone models, which do make use of contextual information.

2. Aligning audio with the acoustic models

The parameters of the acoustic model are estimated in acoustic training steps; however, the process can be better optimized by cycling through training and alignment phases. This is also known as Viterbi training (related, but more computationally expensive procedures include the Forward-Backward algorithm and Expectation Maximization). By aligning the audio to the reference transcript with the most current acoustic model, additional training algorithms can then use this output to improve or refine the parameters of the model. Therefore, each training step will be followed by an alignment step where the audio and text can be realigned.

3. Triphone models

While monophone models simply represent the acoustic parameters of a single phoneme, we know that phonemes will vary considerably depending on their particular context. The triphone models represent a phoneme variant in the context of two other (left and right) phonemes.

At this point, we’ll also need to deal with the fact that not all triphone units are present (or will ever be present) in the dataset. There are (# of phonemes)3 possible triphone models, but only a subset of those will actually occur in the data. Furthermore, the unit must also occur multiple times in the data to gather sufficient statistics for the data. A phonetic decision tree groups these triphones into a smaller amount of acoustically distinct units, thereby reducing the number of parameters and making the problem computationally feasible.

4. Re-aligning audio with the acoustic models & re-train triphone models

5. Neural Models

The Acoustic modelling in Kaldi is mono+tri+DNN. (Need to update)

I will keep you posted about my progress!

### Others

- [My GSoC 2019 Journey](https://aashishag.github.io/categories/#gsoc)
- [Repository of Code](https://github.com/AASHISHAG/asr-german)