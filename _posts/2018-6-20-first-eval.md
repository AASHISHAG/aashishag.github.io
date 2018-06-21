---
title:  "GSoC First Evaluation"
date:   2018-6-20
layout: single
author_profile: true
comments: true
tags: [GSoC, AVSR]
category: GSoC
---

So it has nearly been a month since the start of official coding period (14th of May) and I successfully passed the first evalution! :wink:
Here I will try to break down what all things were done in that period. 

Most of the cummunity bonding period was utilised in getting access to the Case Western Reserve HPC servers and understanding the work done by the previous year GSoC candidate [Divesh Pandey](https://github.com/pandeydivesh15/AVSR-Deep-Speech) in the same domain of Audio Visual Speech Recognition (AVSR).

First coding month went mostly in understanding the case of handling current speaker in a video when there are multiple faces in a video and in devising the architecture of the model. So I will divide the work summary in two, accordingly.

### Multiple Speaker Detection Case

Most of the prior work done in identifying the right speaker in a video frame in case of multi-speaker was either done by training a supervised model having labelled data separated by each speaker eg. the paper previously mentioned in my proposal, [Deep Multimodal Speaker Naming](https://arxiv.org/abs/1507.04831). Image shown below,

![](https://herohuyongtao.github.io/publications/speaker-naming/teaser.png)

Or by following some non-Machine Learning based methods such as finding mean squared difference of pixels of detected face region in consequetive frames, as followed by Divesh previously and stated in the paper, [Automatic
Naming of Characters in TV Video](http://www.robots.ox.ac.uk/~vgg/publications/papers/everingham06a.pdf)

The problem with first approach was getting labelled data for each speaker with can be costly and even if we somehow manage it our model won't be able to generalise on faces that it haven't seen before. As stated by Divesh the second method wasn't robost enough and there were some false positive cases.

Solution to this type of problem where we didn't had access to labelled data was found in the paper, [Out of time: automated lip sync in the wild
](http://www.robots.ox.ac.uk/~vgg/software/lipsync/). Video demo [here](https://youtu.be/AAVZDhGld0U?t=28).

Model architecture shown below, 

![](https://media.springernature.com/lw785/springer-static/image/chp%3A10.1007%2F978-3-319-54427-4_19/MediaObjects/426014_1_En_19_Fig2_HTML.gif)

Though originally trained to detect offset of audio lag in a video but taking input of mouth cropped images and corresponding audio and then minimizing constrastive loss function to minimize l2 distance between visual and audio embeddings from fc7 layers for positive pairs and maximize for negative pairs.

Hence a case of speaker detection can be thought of a positive pair for a face of actual speaker and corresponding audio during that time-stamp of video and negative pairs for all other detected faces and the same audio. The pair having a minimum l2 distance between mouth region and audio embeddings will be the one of actual speaker.

Luckily the author of original paper open sourced his model just a week before I started working on! Here's the original [repo](https://github.com/joonson/syncnet_python). The original repo did not included the case of multi-speaker detection hence I build upon the existing code base to include it, check "run_speaker.py" in the forked repo [here](https://github.com/ajinkyaT/Lip_Reading_in_the_Wild_AVSR/tree/master/SyncNet).

Here's a [demo output](https://drive.google.com/open?id=1xCAmJJpEXLPThxo-L8lx_t_JtP5MZSaz) after running "run_speaker.py"

### Proposed Plan Ahead

Even though I initially planned on using Deep Speech 2 model as an enhancement for Audio Speech Recognition and later fuse visual modality with it but then I decided to deviate from Deep Speech 2 after I discovered this wonderful paper , [Lip Reading Sentences in the Wild      (LRW)](https://arxiv.org/abs/1611.05358) released by Google's DeepMind. 

There were many reasons in doing that some of the improvements which Deep Speech 2 lacked and were offered by LRW are:

- Deep Speech was originally trained as Audio Speech Recognition whereas LRW was trained as completely end to end Audio Video Speech Recognition model which is our end goal.
- Deep Speech uses CTC loss function and lacks general seq2seq with attention architecture. As author in the paper mentions, "For the most part, prior work can be divided into two types. The first type uses CTC, where the model typically predicts framewise labels and then looks for the optimal alignment between the framewise predictions and the output sequence. The weakness is that the output labels are not conditioned on each other. The second type is sequence-to-sequence models that first read all of the input sequence before starting to predict the output sentence. A number of papers have adopted this approach for speech recognition, and the most related work to ours is that of Chan et al. which proposes an elegant sequence-to-sequence method to transcribe audio signal to characters. They utilise a number of the latest sequence learning tricks such as scheduled sampling and attention; we take many inspirations from this work."
- I had also mentioned [LipNet](https://arxiv.org/abs/1611.01599) in the proposal which is Video only Speech Recognition model from lip movements with no support for audio speech recognition. Again this model too lacks general seq2seq with attention mechanism and relies on CTC loss function which stated earlier is known to underperform compared to seq2seq with attention ones.

So after having decided to go with implementing LRW sentences model I faced with another challenge that there isn't any open source implemnetation of the model available yet! That means I have to implement it all by myself from building data-processing pipeline to model building and training which may seem daunting at first but is also quite exciting as I will get to learn about executing a Machine Learning project end-to-end which is a rare opportunity to come by. :smirk:

As discussed with my mentor Karan, we first decided to focus on visual modadlity part as audio modality is relatively easier to build and there are open source implementations available online too! like this one, [Listen, Attend and Spell](https://github.com/thomasschmied/Speech_Recognition_with_Tensorflow), link to paper [here](https://arxiv.org/abs/1508.01211). Also instead of training whole model we decided to first train the visual encoder part to classify the sentences from [MIRACL-VC1](https://sites.google.com/site/achrafbenhamadou/-datasets/miracl-vc1) dataset. And then extend the same network to have decoder part trained. Model for encoder part will look like below:

![](https://media.springernature.com/lw785/springer-static/image/chp%3A10.1007%2F978-3-319-54427-4_19/MediaObjects/426014_1_En_19_Fig10_HTML.gif)

I hope to complete the training of Visual Encoder part before my second evaluation till then happy coding! :smiley: