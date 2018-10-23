---
title:  "Collection of online resources for AVSR"
date:   2018-7-08
layout: single
author_profile: true
comments: true
tags: [GSoC, AVSR]
category: GSoC
toc: true
toc_label: "Resources"
toc_icon: "heart"
---

![](/others/GSOC.png)

## Collection of online resources for AVSR

### Papers and implementations

Below is the collection of papers, datasets, projects I came across while searching for resources for Audio Visual Speech Recognition.

Paper I am trying to implement, [Lip Reading Sentences in the Wild](https://arxiv.org/abs/1611.05358).

[PyTorch implementation of SyncNet](https://github.com/joonson/syncnet_python) based on paper, [Out of time: automated lip sync in the wild](http://www.robots.ox.ac.uk/~vgg/software/lipsync/) Keras implementation [here](https://github.com/voletiv/syncnet-in-keras).

[Keras implementation of LipNet](https://github.com/rizkiarm/LipNet) based on paper, [LipNet: End-to-End Sentence-level Lipreading](https://arxiv.org/abs/1611.01599).

[Lip Reading in the Wild using ResNet and LSTMs in Torch
](https://github.com/tstafylakis/Lipreading-ResNet) based on paper, [Combining Residual Networks with LSTMs for Lipreading
](https://arxiv.org/abs/1703.04105) PyTorch implementation of same, [Lip Reading in the Wild using ResNet and LSTMs in PyTorch
](https://github.com/psyec1/Lipreading-PyTorch)

Not a speech to text system but to match lip video with corresponding audio. [Lip Reading - Cross Audio-Visual Recognition using 3D Architectures in TensorFlow](https://github.com/astorfi/lip-reading-deeplearning) based on paper, [3D Convolutional Neural Networks for Cross Audio-Visual Matching Recognition](https://ieeexplore.ieee.org/document/8063416/).

[Keras implementation of Vid2speech](https://github.com/arielephrat/vid2speech) based on paper, [Vid2Speech: Speech Reconstruction from Silent Video](https://arxiv.org/abs/1701.00495) project site [here](http://www.vision.huji.ac.il/vid2speech/).

[TensorFlow implementation of a seq2seq model for Speech Recognition](https://github.com/thomasschmied/Speech_Recognition_with_Tensorflow) not a visual speech recognition but audio speech recognition based on paper, [Listen, Attend and Spell](https://arxiv.org/abs/1508.01211). This was an improvement over DeepSpeech by using seq2seq architecture with attention mechanism. Also the architecture is similar to the audio only part of Lip Reading Sentences in the Wild (LRW) model.

A recently released paper from the authors of lip reading in the wild and lip reading using ResNet, [Deep Lip Reading: a comparison of models and an online application](https://arxiv.org/abs/1806.06053). The focus is on using Spatio-Temporal 3D CNN to extract visual features.

### Datasets

[Miracl VC-1 corpus](https://sites.google.com/site/achrafbenhamadou/-datasets/miracl-vc1). Fifteen speakers utter ten times a set of ten words and ten phrases (see the table below):

![](https://raw.githubusercontent.com/deepconvolution/LipNet/master/category.png)

[Lip Reading in the Wild (LRW) words dataset](http://www.robots.ox.ac.uk/~vgg/data/lip_reading/), The dataset consists of up to 1000 utterances of 500 different words, spoken by hundreds of different speakers. All videos are 29 frames (1.16 seconds) in length. (Need to obtain permission before downloading)

[Lip Reading in the Wild (LRW) sentences dataset](http://www.robots.ox.ac.uk/~vgg/data/lip_reading_sentences/), The dataset consists of thousands of spoken sentences from BBC television. Each sentences is up to 100 characters in length. (Need to obtain permission before downloading)

[The GRID audiovisual sentence corpus](http://spandh.dcs.shef.ac.uk/gridcorpus/) the corpus consists of high-quality audio and video (facial) recordings of 1000 sentences spoken by each of 34 talkers (18 male, 16 female). Sentences are of the form "put red at G9 now".  The corpus is together with transcriptions.
