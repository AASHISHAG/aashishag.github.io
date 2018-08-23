---
title:  "GSoC 2018 - Audio-Visual Speech Recognition using Deep Learning"
date:   2018-8-13
layout: single
author_profile: true
comments: true
tags: [GSoC, AVSR]
category: GSoC
toc: true
toc_label: "Contents"
toc_icon: "heart"
---

![](/others/GSOC.png)

Link to [Repository of Code](https://github.com/ajinkyaT/Lip_Reading_in_the_Wild_AVSR)

### Describe my work briefly

- Study previous work done by GSoC 2017 candidate and propose improvements
- Implement speaker recognition in a video using audio-visual modalities without having any labelled training data (SyncNet)
- Implement completely end to end Audio Visual Speech recognition pipeline by using the model described in the paper [Lip Reading Sentences in the Wild](https://arxiv.org/abs/1611.05358)

### What is done

- Doing a literature review to identify state-of-the art implementations for Audio-Visual Speech Recognition
- Speaker recognition in a video by using the model, [Out of time: automated lip sync in the wild (SyncNet)](http://www.robots.ox.ac.uk/~vgg/software/lipsync/)
- LRW-Sentences model architecture defined by using TensorFlow
- Data processing pipeline to process visual data and make batches of visual cube tensors mentioned in the paper for passing them into Convolutional Neural Network 

### TODO

- Integrate visual processing pipeline as an input to the model by using new tf.data API
- Performing training and validation using just a visual data, as mentioned in the, "Watch-Attend-Spell" section of the paper
- Add support for audio part mentioned in the section, "Listen-Attend-Spell" of the paper

### Future directions

- Training or LRW is currently performed on the [The GRID audiovisual sentence corpus](http://spandh.dcs.shef.ac.uk/gridcorpus/) which has near same recording environment for every speaker this could further be improved upon by using data having varied background location like news videos
- Currently Speaker recognition in a video frame (SyncNet) and LRW Sentences are two separate implementations; this could be brought under single roof so that AVSR model works even in the cases where there are multiple speakers in the video frame
- CNN architecture used for extracting visual features was that of VGG-M but recent work research suggests using ResNet for better performance as mentioned in the paper, [Combining Residual Networks with LSTMs for Lipreading
](https://arxiv.org/abs/1703.04105)

### Others

- [My GSoC 2018 Journey](https://ajinkyat.github.io/categories/#gsoc)
- [Repository of Code](https://github.com/ajinkyaT/Lip_Reading_in_the_Wild_AVSR)
- [My proposal for the project](https://github.com/ajinkyaT/GSOC_Red_Hen_Lab/blob/master/Ajinkya_Proposal_for_AVSR.md)
