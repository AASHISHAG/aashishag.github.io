---
title:  "Week 10 + Week 11 (ASR - German)"
date:   2019-8-12
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

Still updating ..... 

I am happy to update on my Week 10 and Week 11 progress. This period was the most exciting period. I spent time training and evaluatig the model and finally running it on CASE HPC.

### Training
This was the most crucial part. I arranged all the modules namely, MFCC Features, Acoustic Model and Language Model and tested the sequence on a smaller dataset, before putting the model on training on the complete data. The training took a long time to complete and finally it was 100%.

``` bash
[steps/nnet3/chain/train.py:519 - train - INFO ] Iter: 5472/5483   Jobs: 1   Epoch: 3.99/4.0 (99.8% complete)   lr: 0.000101   shrink: 0.99799
[steps/nnet3/chain/train.py:519 - train - INFO ] Iter: 5473/5483   Jobs: 1   Epoch: 3.99/4.0 (99.8% complete)   lr: 0.000100   shrink: 0.99799
[steps/nnet3/chain/train.py:519 - train - INFO ] Iter: 5474/5483   Jobs: 1   Epoch: 3.99/4.0 (99.8% complete)   lr: 0.000100   shrink: 0.99799
[steps/nnet3/chain/train.py:519 - train - INFO ] Iter: 5475/5483   Jobs: 1   Epoch: 3.99/4.0 (99.8% complete)   lr: 0.000100   shrink: 0.99799
[steps/nnet3/chain/train.py:519 - train - INFO ] Iter: 5476/5483   Jobs: 1   Epoch: 3.99/4.0 (99.9% complete)   lr: 0.000100   shrink: 0.99799
[steps/nnet3/chain/train.py:519 - train - INFO ] Iter: 5477/5483   Jobs: 1   Epoch: 3.99/4.0 (99.9% complete)   lr: 0.000100   shrink: 0.99799
[steps/nnet3/chain/train.py:519 - train - INFO ] Iter: 5478/5483   Jobs: 1   Epoch: 4.00/4.0 (99.9% complete)   lr: 0.000100   shrink: 0.99799
[steps/nnet3/chain/train.py:519 - train - INFO ] Iter: 5479/5483   Jobs: 1   Epoch: 4.00/4.0 (99.9% complete)   lr: 0.000100   shrink: 0.99800
[steps/nnet3/chain/train.py:519 - train - INFO ] Iter: 5480/5483   Jobs: 1   Epoch: 4.00/4.0 (99.9% complete)   lr: 0.000100   shrink: 0.99800
[steps/nnet3/chain/train.py:519 - train - INFO ] Iter: 5481/5483   Jobs: 1   Epoch: 4.00/4.0 (99.9% complete)   lr: 0.000100   shrink: 0.99800
[steps/nnet3/chain/train.py:519 - train - INFO ] Iter: 5482/5483   Jobs: 1   Epoch: 4.00/4.0 (100.0% complete)   lr: 0.000100   shrink: 0.99800
[steps/nnet3/chain/train.py:519 - train - INFO ] Iter: 5483/5483   Jobs: 1   Epoch: 4.00/4.0 (100.0% complete)   lr: 0.000100   shrink: 0.99800
[steps/nnet3/chain/train.py:575 - train - INFO ] Doing final combination to produce final.mdl
```

### Results

<audio controls>
  <source src="/others/de_1.wav" type="audio/wav">
</audio>

``` bash
$ Gerrit erinnerte sich daran dass er einst einen Eid geschworen hatte
$ Garrett erinnerte sich daran dass er einst einen Eid geschworen hatte
```

<audio controls>
  <source src="/others/de_2.wav" type="audio/wav">
</audio>

``` bash
$ Wenn man schnell fährt ist man von Emden nach Landshut nicht lange unterwegs
$ Weil man schnell fährt ist man von Emden nach Landshut nicht lange unterwegs
```

<audio controls>
  <source src="/others/de_3.wav" type="audio/wav">
</audio>

``` bash
$ Valentin hat das Handtuch geworfen
$ Valentin hat das Handtuch geworfen
```

<audio controls>
  <source src="/others/de_4.wav" type="audio/wav">
</audio>

``` bash
$ Auf das was jetzt kommt habe ich nämlich absolut keinen Bock
$ Auf das was jetzt kommt habe ich nämlich absolut keinen Bock
```

<audio controls>
  <source src="/others/de_5.wav" type="audio/wav">
</audio>

``` bash
$ Ich könnte eine Mitfahrgelegenheit nach Schweinfurt anbieten
$ Ich könnte eine Mitfahrgelegenheit nach Schweinfurt anbieten
```

<audio controls>
  <source src="/others/de_6.wav" type="audio/wav">
</audio>

``` bash
$ Man sollte den Länderfinanzausgleich durch einen Bundesligasoli ersetzen
$ Man sollte den Länderfinanzausgleich durch ein Bundesliga Soli ersetzen
```

<audio controls>
  <source src="/others/de_7.wav" type="audio/wav">
</audio>

``` bash
$ Von Salzburg ist es doch nicht weit bis zum Chiemsee
$ Von Salzburg ist es doch nicht weit Bistum Chiemsee
```

<audio controls>
  <source src="/others/de_8.wav" type="audio/wav">
</audio>

``` bash
$ Selbst für den erfahrensten Chirurgen ist der Tumor eine knifflige Herausforderung
$ Selbst für den erfahrensten Chirurgen ist der Tumor eine knifflige raus Federung
```

<audio controls>
  <source src="/others/de_9.wav" type="audio/wav">
</audio>

``` bash
$ Folgende Lektüre kann ich ihnen zum Thema Kognitionspsychologie empfehlen
$ Folgende Lektüre kann ich ihn zum Thema Kognitionspsychologie empfehlen
``` 

<audio controls>
  <source src="/others/de_10.wav" type="audio/wav">
</audio>

``` bash
$ Warum werden da keine strafrechtlichen Konsequenzen gezogen
$ Warum werden da keine strafrechtlichen Konsequenzen gezogen
```

### CASE HPC


### Others

- [My GSoC 2019 Journey](https://aashishag.github.io/categories/#gsoc)
- [Repository of Code](https://github.com/AASHISHAG/asr-german)