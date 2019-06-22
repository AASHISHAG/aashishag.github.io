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

I am happy to update on my Week 2 and Week 3 progress. These two weeks were crucial, I was working on data pre-processing and computing standard 13-dimensional Mel-Frequency Cepstral Coefficients (MFCC) features of the speech data.

### Installing Kaldi ...

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
``` bash





Week 4 and Week 5 is the evaluation period. I will take feedback from mentors and bring improvements in my task. The first task would be to build the German phoneme dictionary. The data is not readily available. I approach to use the scripts provided by the researchers at Hamburg University, Germany. The technique needs to be verified and some bottlenecks are expected.

I will keep you posted about my progress!

### Others

- [My GSoC 2019 Journey](https://aashishag.github.io/categories/#gsoc)
- [Repository of Code](https://github.com/AASHISHAG/asr-german)
