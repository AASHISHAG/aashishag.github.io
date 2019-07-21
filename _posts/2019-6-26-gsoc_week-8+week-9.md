---
title:  "Week 8 + Week 9 (ASR - German)"
date:   2019-7-24
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

I am happy to update on my Week 8 and Week 9 progress. This period was challenging. I spent this period working on integrating all the modules to create an end-to-end Automatic Speech Recognition pipeline and resolving the issues.

Automatic Speech Recognition pipeline has four significant steps:

1. Pre-Processing
2. Feature Extraction
3. Language Model
4. Acoustic Model

The following is depicted in the image below:

![](
/others/speech-recognition-pipeline.png)

To work with German dataset, care has to be taken that the scripts are UTF-8 compatible. While most of the example scripts from Kaldi supports UTF-8, there are several that are still in ASCII format. When working on integrating all the above modules, the code produced a lot of issues. Since the bugs were logged on a high level, they were difficult to debug. Also, overtime Kaldi is adapting Python 3, but still many scripts support only Python 2. This was challenging, while I had implemented the pipeline in Python 3. Apart from them, there were other specific data issues. 

I would like to thanks the open community of developers and [Kaldi help group](https://groups.google.com/forum/#!forum/kaldi-help) for the guidance. 

Now, I have created an end-to-end German ASR pipeline. Next week I would keep the model on training. Keeping my fingers crossed.

I will keep you posted about my progress!

### Others

- [My GSoC 2019 Journey](https://aashishag.github.io/categories/#gsoc)
- [Repository of Code](https://github.com/AASHISHAG/asr-german)