---
title:  "Week 12 + Week 13 (ASR - German)"
date:   2019-8-26
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

I am happy to update on my Week 12 and Week 13 progress. I utilized this period to create the German Speech Pipeline and format the transcripts in Red Hen's Data Format and document my work.

### Kaldi-Gstreamer-Server

I used [Kaldi-Gstreamer-Server](https://github.com/alumae/kaldi-gstreamer-server) to run the model on HPC. This is a real-time full-duplex speech recognition server, based on the Kaldi toolkit and the GStreamer framework and implemented in Python. It also provides an API where audio can post to get real-time transcripts. Kaldi-Gstreamer-Server helped to avoid using VAD (Voice Activity Detection) toolkit, as it automatically splits the audio in small clips of length 8 seconds each and pushes it to Kaldi for Speech Transcription. It is thus producing a continuous speech transcription.

I created scripts to automatically load the Singularity module, run the GStreamer server, worker, and push the audio to Kaldi. The scripts can be found at GitHub. Execute the following sequence of steps:

``` bash
$ ./run-server.sh
$ ./run-worker.sh
$ ./run-model.sh path_audio_clip
``` 

### German Speech Pipeline

The last task was to create a German Speech Pipeline, that can transcribe Red Hen's News Dataset. I created a Pipeline that automatically picks the Red Hen's German News for a given day, converts it to WAV, transcribes it, and finally formats the data in [Red Hens Data Format](https://sites.google.com/site/distributedlittleredhen/home/the-cognitive-core-research-topics-in-red-hen/red-hen-data-format#TOC-Audio-Pipeline-Tags) adding appropriate Headers and Footers.

I took inspiration from Red Hen's Chinese Speech Pipeline to achieve this daunting task, and I want to thank Ziyi Liu for appropriate guiding. 

``` bash
$ ./run-server.sh
$ ./run-worker.sh
$ ./kaldi_de.sh
``` 

This is a small excerpt from the Red Hen News Dataset. The MP4 files are programmatically converted to WAV and fed to Kaldi-Gstreamer-Server. The model output, i.e., the transcripts are further formatted to adopt [Red Hen's Data Format](https://sites.google.com/site/distributedlittleredhen/home/the-cognitive-core-research-topics-in-red-hen/red-hen-data-format#TOC-Audio-Pipeline-Tags).
    
``` bash    
TOP|20190812180001|2019-08-12_1800_DE_DasErste_Tagesschau
COL|Communication Studies Archive, UCLA
UID|3ef55370-bd2d-11e9-95d1-b78b1645001f
DUR|00:14:54
VID|720x576|640x512
SRC|Osnabruck, Germany
CMT|Evening news
CC1|DEU 150
ASR_01|DE
20190812180010.000|20190812180013.760|CC1|Hier ist das Erste Deutsche Fernsehen mit der tagesschau.
ASR_01|2019-08-15 08:34|Source_Program=Kaldi,infer.sh|Source_Person=Aashish Agarwal|Codebook=Deutsch Speech to Text
20190812180014.280|20190812180024.280|ASR_01|So ist es die erste deutsche Fernsehen mit der Tagesschau. Heute im Studio Jan Hofer Nama der Damen und Herren ich begrüße sie zwei Tage. Bundesumweltministerin Schultze will die Hersteller von wegwerfen Artikeln künftig an den Kosten für die Müllbeseitigung beteiligen die es für die Politiker werden stellt ihre Pläne heute in Berlin vor Die sprach von einer regelrechten Müll Flut in manchen Städten Ziel sei eine finanzielle Entlastung der Kommunen und ein Umdenken in der Gesellschaft betroffen werden. <UNK> anderem Firmen sein die Verpackungen Getränke Becher Plastiktüten und Zigaretten Filter produzieren. Alltag auf deutschen Straßen. Reste der wegwerfen Gesellschaft. Für die Aufräumarbeiten Zahlen Städte und Gemeinden. Die Bundesumweltministerin will die Kommunen entlasten mit Geld das sie bei den Herstellern der wegwerfen Artikel eintreiben möchte. Heißt das Sie müssen für das Einsammeln dieser Produkte zahlen sie müssen sich anteilsmäßig an den Kosten für das Aufstellen von Abfall Behältern Beteiligungen ebenso müssen sich diese Hersteller an den Kosten für die Entsorgung beziehungsweise das Recycling beteiligen damit setzt wenn ihr Schulz für eine EU Richtlinie. Der Koalitionspartner aber sorgt das ginge auch anders ohne eine Zusatzbelastungen der Verpackungsindustrie
END|20190812181455|2019-08-12_1800_DE_DasErste_Tagesschau
```

This ends my 13 weeks journey at [Red Hen Lab](http://www.redhenlab.org/home) for GSoC-2019. I enjoyed working with the team, and I learned a lot solving the challenges. I want to specially thanks to my mentor Dr. Jan Gorisch for providing valuable comments and guiding me over my journey!

I hope you enjoyed reading my blogs!!

### Others

- [My GSoC 2019 Journey](https://aashishag.github.io/categories/#gsoc)
- [Repository of Code](https://github.com/AASHISHAG/asr-german)