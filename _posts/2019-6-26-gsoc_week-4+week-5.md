---
title:  "Week 4 + Week 5 (ASR - German)"
date:   2019-6-26
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

I am happy to update on my Week 4 and Week 5 progress. I am progressing well with the project as per the proposal. This would be the evaluation period. I am totally excited.

### Language Modeling
For language modeling, we will use "German speech data corpus". The corpus is of approximately 8 million German sentences. MaryTTS is used to normalize the text to a form that is close to how a reader would speak the sentence, e.g. any numbers and dates have been converted into a canonical text form and any punctuation has been discarded. The corpus is appropriately filtered so that sentences from the development and test speech corpus are not included in the LM.

### Phoneme Dictionary
Large German phoneme dictionary has strict licensing issues. The researchers at the University of Hamburg, Germany have written some scripts to combine several small phoneme dictionaries. The final dictionary covers 44.8k unique German words with 70k total entries, with alternate pronunciations for some of the more common words. The pronunciation dictionary is of reasonable size for large-vocabulary speech recognition I will keep you posted about my progress. 

### Others

- [My GSoC 2019 Journey](https://aashishag.github.io/categories/#gsoc)
- [Repository of Code](https://github.com/AASHISHAG/asr-german)