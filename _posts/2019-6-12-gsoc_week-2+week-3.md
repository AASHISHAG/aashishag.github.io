---
title:  "Week 2 + Week 3 (ASR - German)"
date:   2019-6-12
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

I am happy to update on my Week 2 and Week 3 progress. These two weeks were crucial. I was working on data pre-processing, and computing standard 13-dimensional Mel-Frequency Cepstral Coefficients (MFCC) features of the speech data.

### Kaldi Installation

It all started with the installation of Kaldi and the requisites. Kaldi installation which looks seemingly straightforward; proved to be quite challenging. The documentation is not straight forward. I witnessed many errors. I resolved a few errors by referring, and for a few, I had to re-install Kaldi all together, which every time took 4-5 hours to install depending on the server configurations. I managed to document all the necessary steps on [GitHub](https://github.com/AASHISHAG/asr-german).

### Data Pre-Processing

A pre-processing module needs to be scripted to achieve the goal. Further, a manifest for the audio and transcripts needs to be created, and data need to be structured to feed them to Kaldi MFCC feature extraction module. It's necessary to arrange the data according to Kaldi's format.

``` bash
(env) agarwal@:~/backup/kaldi-trunk/egs/recipe_v1/data/train$ tree
.
├── cmvn.scp
├── feats.scp
├── frame_shift
├── segments
├── spk2utt
├── text
├── utt2dur
├── utt2num_frames
├── utt2spk
└── wav.scp
```

I utilized several scripts from Kaldi Wall Street Journal (WSJ), Tedlium, and Tuda-De project.

### MFCC Generation

Feature extraction is the most critical step in any ASR. The scripts from Kaldi can be used to compute the speech data as standard 13-dimensional Mel-Frequency Cepstral Coefficients (MFCC) features. I managed to use the scripts from the Wall Street Journal Project (WSJ)

``` bash
steps/compute_cmvn_stats.sh data/$train_data exp/make_mfcc/$x $mfccdir 
```

Output:

``` bash
(env) agarwal@:~/backup/kaldi-trunk/egs/recipe_v1/exp/make_mfcc/dev$ tree
.
├── cmvn_dev.log
├── make_mfcc_dev.1.log
├── make_mfcc_dev.2.log
├── make_mfcc_dev.3.log
├── make_mfcc_dev.4.log
└── make_mfcc_dev.5.log

```


Week 4 and Week 5 is the evaluation period. I will take feedback from mentors and bring improvements to my task. The first task would be to build the German phoneme dictionary. The data is not readily available. I approach to use the scripts provided by the researchers at Hamburg University, Germany. The technique needs to be verified, and some bottlenecks are expected.

I will keep you posted about my progress!

### Others

- [My GSoC 2019 Journey](https://aashishag.github.io/categories/#gsoc)
- [Repository of Code](https://github.com/AASHISHAG/asr-german)
