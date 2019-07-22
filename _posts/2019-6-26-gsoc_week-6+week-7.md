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

The acoustic models are created by training the models on acoustic features from labeled data, i.e., the transcribed speech corpus. Kaldi provides tremendous flexibility and power to train our acoustic models.

To train an end-to-end ASR pipeline, we need:

1.Monophone Models

A monophonic model is an acoustic model that does not include any contextual information about the preceding or the following phone. It is used as a building block for the triphone models, which make use of contextual information.

2.Aligning Audio with the Acoustic Model

The parameters of the acoustic model are estimated in acoustic training steps; however, the process can be better optimized by cycling through training and alignment phases. By aligning the audio to the reference transcript with the most current acoustic model, additional training algorithms can then use this output to improve or refine the parameters of the model. Therefore, each training step will be followed by an alignment step where the audio and text can be realigned.

3.Triphone Model

While monophonic models represent the acoustic parameters of a single phoneme, we know that phonemes will vary considerably depending on their particular context. The triphone models represent a phoneme variant in the context of two other (left and right) phonemes.

At this point, we’ll also need to deal with the fact that not all triphone units are present (or will ever be present) in the dataset. Furthermore, the unit must also occur multiple times in the data to gather sufficient statistics for the data. A phonetic decision tree groups these triphones into a smaller amount of acoustically distinct units, thereby reducing the number of parameters and making the problem computationally feasible.

4.Re-aligning Audio with the Acoustic model

5.Neural Models

Finally, DNN model is implemented to train the model on the aligned data.

This was a brief introduction to the work I did during this period. Next step is to integrate all these pieces.

I will keep you posted about my progress!

### Others

- [My GSoC 2019 Journey](https://aashishag.github.io/categories/#gsoc)
- [Repository of Code](https://github.com/AASHISHAG/asr-german)