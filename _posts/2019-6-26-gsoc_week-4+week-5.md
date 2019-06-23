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

This period was full of unpredictable challenges. I witnessed several issues, not just with configurations but also with Kaldi. Since, we are working with German dataset the encoding has to be changed from ASCII to UTF-8, but several Kaldi scripts still supports ASCII format. I have opened a BUG at the Kaldi forum [google group](https://groups.google.com/forum/#!forum/kaldi-help). The Kaldi's developer Dan Povey merged a PR to resolve the issue but later other scripts started giving errors. I am debugging to resolve the issue.

![](
/others/kaldi-help.PNG)

``` bash
# Started at Thu Jun 13 05:11:24 CEST 2019
#
Traceback (most recent call last):
  File "steps/cleanup/internal/taint_ctm_edits.py", line 247, in <module>
    ProcessData()
  File "steps/cleanup/internal/taint_ctm_edits.py", line 154, in ProcessData
    first_line = f_in.readline()
  File "/media/data/agarwal/python-environments/env3.5.2/lib/python3.5/encodings/ascii.py", line 26, in decode
    return codecs.ascii_decode(input, self.errors)[0]
UnicodeDecodeError: 'ascii' codec can't decode byte 0xc3 in position 303: ordinal not in range(128)
# Accounting: time=1 threads=1
```


I will keep you posted about my progress. 

### Others

- [My GSoC 2019 Journey](https://aashishag.github.io/categories/#gsoc)
- [Repository of Code](https://github.com/AASHISHAG/asr-german)