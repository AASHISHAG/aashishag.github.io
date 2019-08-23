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

I used [Kaldi-Gstreamer-Server](https://github.com/alumae/kaldi-gstreamer-server) to run the model on HPC. This is a real-time full-duplex speech recognition server, based on the Kaldi toolkit and the GStreamer framework and implemented in Python. It also provides an API where audio can post to get real-time transcripts. Kaldi-Gstreamer-Server automatically splits the audio in small clips of length 8 seconds each and pushes it to Kaldi for Speech Transcription. It is thus producing a continuous speech transcription.

I created scripts to automatically load the Singularity module, run the GStreamer server, worker, and push the audio to Kaldi. The scripts can be found at GitHub. Execute the following sequence of steps:

``` bash
$ ./run-server.sh
$ ./run-worker.sh
$ ./run-model.sh path_audio_clip
``` 

### German Speech Pipeline

The last task was to create a German Speech Pipeline, that can transcribe Red Hen's News Dataset. I created a Pipeline that automatically picks the Red Hen's German News for a given day, converts it to WAV, transcribes it, and finally formats the data in [Red Hens Data Format](https://sites.google.com/site/distributedlittleredhen/home/the-cognitive-core-research-topics-in-red-hen/red-hen-data-format#TOC-Audio-Pipeline-Tags) adding appropriate Headers and Footers.

I took inspiration from Red Hen's Chinese Speech Pipeline to achieve this daunting task, and I want to thank Ziyi Liu for appropriate guiding. 

I implemented two solutions for Red Hen's News dataset transcription.

1. Continuous Speech Transcription.
2. Speech Transcript using Voice Activity Detection (VAD)

I used [WebrtcVAD](https://github.com/wiseman/py-webrtcvad) to split long audio clips into smaller clips. This is a python interface to the WebRTC Voice Activity Detector (VAD). A [VAD](https://en.wikipedia.org/wiki/Voice_activity_detection) classifies a piece of audio data as being voiced or unvoiced. 

![](
/others/speech-recognition-pipeline-3.png)

``` bash
$ ./run-server.sh
$ ./run-worker.sh
$ ./model-run.slurm specify_the_number_of_days_from_the_current_date_the_model_should_transcribe
$ ./run-model-vad.slurm specify_the_number_of_days_from_the_current_date_the_model_should_transcribe
``` 

This is a small excerpt from the Red Hen News Dataset. The MP4 files are programmatically converted to WAV and fed to Kaldi-Gstreamer-Server. The model output, i.e., the transcripts are further formatted to adopt [Red Hen's Data Format](https://sites.google.com/site/distributedlittleredhen/home/the-cognitive-core-research-topics-in-red-hen/red-hen-data-format#TOC-Audio-Pipeline-Tags).
    
**_Continuous Speech Transcript_**
    
``` bash    
TOP|20190817150002|2019-08-17_1500_DE_DasErste_Tagesschau
COL|Communication Studies Archive, UCLA
UID|29979bf0-c101-11e9-a5ab-3bdd627efb4b
DUR|00:09:54
VID|720x576|640x512
SRC|Osnabruck, Germany
CMT|Afternoon news
CC1|DEU 150
ASR_02|DE
20190817150009.960|20190817150013.720|CC1|Hier ist das Erste Deutsche Fernsehen mit der tagesschau.
ASR_02|2019-08-19 14:07|Source_Program=Kaldi,infer.sh|Source_Person=Aashish Agarwal|Codebook=Deutsch Speech to Text
20190817150014.280|20190817150024.280|ASR_02|In Ungarn den Änderungen in den Bodensee ist es jetzt den deutschen Fernsehsendern wie der Tagesschau. Sie im Studio Karolinen lernen. Meine Damen und Herren ich begrüße Sie zutage Schau. Die Tiere in Berlin findet oft hinter verschlossenen Türen statt an diesem Wochenende aber stehen viele Türen offen Politik wird dann zwar nicht gemacht aber die Bürger sind eingeladen sich über die Arbeit der Bundesregierung zu informieren das Kanzleramt Die Ministerien und das Bundes Presseamt bieten mehr als acht Hundert Veranstaltungen an das Motto in diesem Jahr Halle. Politik. Familienministerin ist heute mit den Kindern aufgestanden macht den Auftakt beim Tag der offenen Tür Demokratie Grundrechte das muss schon bei den kleinsten Thema sein Amt Kinder rechts Bus wissen Sie genau was sie von der Ministerin erwachten Brecht erbaut. <UNK> Gewalt freie entziehen. Das Recht eine Ausbildung zu machen das Recht das Thema des kennen zur Schule gehen kann wenn man Behinderungen hart und so dass man trotzdem gleichberechtigtes heranwachsen. Auch Religionen Kultur und Summers Heute spricht der Bürger die Politiker hören es zu Hallo Politik das Kanzleramt Lied ein und alle vierzehn Ministerien Lassen hinter die Kulissen schauen Andrang und Ausflüge auch in Europas größten danken den hat das Gesundheitsministerium aufstellen lassen die gesund. des Bürgers ist wichtig Aufklärung tut Not und auch die im <UNK> Quoten und so kann wer will sich gleich noch impfen lassen ehe bekommt die zweite Masern Impfung. Alles für Jens Sparten. Bürger fragen Politiker antworten der Finanzminister der auch es Pedell Chef werden will lässt sich auch vom Volk wenig entlocken und nichts zur Pacht nach innen Wahl zur Demokratie dazu dass man sich auch mit <UNK>. Nun Freunden guten spricht und Bambus sagt Wenn was zu sagen ist heute also der Vizekanzler Morgen dann die Kanzlerin. In der C die Ouvertüre über einen Parteiausschluss des früheren Verfassungsschutz Präsidenten Maßen diskutiert Die Vorsitzende Kramp Karrenbauer sagte den Zeitungen der Funke Mediengruppe sie sehe beimaßen keine Haltung die ihn mit der C die EU noch wirklich verbinde Allerdings gebe es hohe Hürden für einen Parteiausschluss Der sächsische Ministerpräsident. Kretschmer kritisierte die Überlegungen Man schließt er niemanden aus der C D U aus nur weil er unbequem sei maßen gilt als konservativer C die EU Politiker und Gegner von Merkels Flüchtlingspolitik. In Hongkong haben erneut Tausende Menschen für Freiheit und Demokratie demonstriert. Hirten vorwiegend Lehrer zum Sitz der umstrittenen Regierungschefin Lärm der Protest verlief friedlich Unterdessen trafen sich in einem Park der Metropole Tausender Gegendemonstranten mit chinesischen Fahnen die sich selbst die Beschützer Hongkongs nennen die Zentralregierung in Peking hatte zuletzt vor Unruhen gewarnt Einheiten der Bewohner. Volkspolizei sind seit Tagen in der DDR benachbarten chinesischen Staat Shannon Jenny stark zunimmt. Im Sudan ist nach langen Verhandlungen der Weg für eine Übergangsregierung frei Vertreter von Opposition und bislang regierende Militär Rat haben heute in der Hauptstadt Khartum ein Abkommen unterzeichnet das einen gemeinsamen Rat von Zivilisten und Militärangehörigen vorsieht Dieser soll etwas mehr als drei Jahre lang. Gießen Dann sollen Wahlen stattfinden. Der Sudan Bäume britische Kolonie und wurde neun Hundert sechsundfünfzig unabhängig politisch stabile Phasen gab es seitdem kaum mehrmals putschte sich das Militär an die Macht. Neun und achtzig der Staatsstreich durch Generalleutnant Baschir der später offiziell Präsident wird unterstützt wird er von Islamisten unter ihrem Einfluss verhängte Baschir ein Scharia Gesetz und verschärfte damit den Konflikt mit dem Süden des Landes in dem das Christentum und traditioneller Religionen verbreitet sind. In bei Schiras Zeit fällt auch der Ausbruch des Darfur Konflikts Regierungstreue Milizen gehen brutal gegen rebellierende Volksgruppen vor ein Hundert Punkt null null null werden getötet der Konflikt ist bis heute nicht gelöst. Internationale Strafgerichtshof verhängte Haftbefehle gegen Baschir unter anderem wegen Kriegsverbrechen und Völkermordes. <UNK> und elf wird der Südsudan unabhängig. Olga stürzt der Sudan in eine wirtschaftliche Krise die zuletzt in immer stärkere Proteste mündet. Dreißig Jahre nach seiner Machtübernahme wird bei schier aus den eigenen Reihen gestürzt die Kontrolle übernimmt ein Militärrat aus allen Landesteilen sind sie nach Khartum gereist um einen historischen Tag zu feiern. Teheran ist nun Geschichte Es beginnt eine neue Ära. De la Rey de kann ich endlich wieder frei durch atmen die den alles war sehr teuer lieferbaren verzweifelt. Zwei Unterschriften festlicher Rahmen und viele Prominente aus dem Ausland Vertreter von Opposition und Militär besiegeln das über Monate mühsam verhandelte Vertrags. Der souveräner Rat ist künftig höchstes Staatsorgan Opposition und Militärs entsenden jeweils fünf Vertreter den elften bestimmen beide einvernehmlich ein General führt zunächst den Vorsitz der Rat überwacht die Regierungsbildung die Opposition benennt den Premierminister. <UNK> Militär den Innen und Verteidigungsminister nach neununddreißig Monaten Gibt es Wahlen. Hara militärischer Gruppen sollen künftig der Armee unterstellt werden Sie haben Anfang Juni ein Protest kennt mit brutaler Gewalt aufgelöst das gab viele Tote eine schwere Bürde Nun soll ein neues Kapitel aufgeschlagen werden. Eine Reihe hoffen dass es mit dem Sudan jetzt aufwärts geht der weder stolzer von Saldanha im können die Waffen niederlegen Frieden schließen können. <UNK> und <UNK>. Für Millionen ist ist der Tag der Freiheit auch wenn auf dem Weg zur Demokratie Unwägbarkeiten bleiben. Der Kult Film Easy Rider hat ihn berühmt gemacht das erste große Roadmovie der Kinogeschichte Eine begeistert gefeiert der Rebellion gegen das U es Establishment der späten sechzig er Jahrgang Peter Fonda wurde damit zum Idol der Hippiebewegung jetzt ist der Schauspieler im Alter von neunundsiebzig Jahren gestorben Nach Angaben seiner. Amelia erlag er den Folgen einer Lungenkrebserkrankung. Diese Leute versuchte er die Freiheit und fand Drogen und Rock n Roll. Von der spielte an der Seite von Bernay Vorfahr vor fünfzig Jahren nicht nur eine Hauptrolle in Easy Rider Er schrieb auch am Drehbuch mit und produzierte. Abenteuerfilm und Gesellschaftskritik zugleich brachte Easy Rider Peter Fonda seine erste Oscar Nominierung ein und machte ihm früher Leinwand Legende die Schauspielerei hatte er in den Genen schon sein Vater Henry Fonda war ein Star auf seine Schwester Jane reüssierte in Hollywood die Mutter hatte sich das Leben genommen als Peter und Jane noch Kind. waren vielleicht auch deshalb lagen Peter Fonda melancholische Räume. Als Bienenzüchter Vietnam Veteranen kämpfte er in dem Film JuLis Gold gegen Kriegs Trauma und Einsamkeit. Hat im Erdreich ihre Einkäufe selbst. Ich mach das Schiff. Ich bin nur so durcheinander. Neun Dingen gegenüber neuen Gefühlen. Ein Menschen. Diese Rolle gewann Fonda dem Golden Globe siebenundzwanzig Jahre nach Easy Rider Kamm Becks wie diese sind selten in Hollywood. Es ist großartig zurück zu sein Gardens ruhige Weberei. Mit einem Stern auf dem Hollywood Boulevard wird er im Filmgeschäft unsterblich auch wenn er im Alter von neunundsiebzig Jahren den Kampf gegen den Lungenkrebs verliert seine Schwester Jane Fonda veröffentlichte eine Stellungnahme in seinen letzten Tagen hatte ich eine schöne Zeit mit ihm allein erging lachend davon. Die Wette Aussichten. Nun wechselnd bewölkt mit sonnigen Abschnitten später vom Südwesten bis in die Mitte Schauer Zum Teil Gewitter die sich Richtung Osten ausbreiten achtzehn bis dreiunddreißig Grad. Die Tagesschau meldet sich wieder um siebzehn Uhr fünfzig Ich wünsche Ihnen einen schönen Tag. Neben Vorlage oder die Sängerin der Banco Bena bei Vala Gong gab. Die Verpflichtung Gagat wahrlich Das ist die Wahl Haupterwerbsquelle verstehen war das sind rein auf dem Tappert Fella aller Verstehen Sie Spaß Marc Forster schmeißt Nepal. Von den ehrlich Brothers ist nur einer ehrlich. Daher habe ich bringe Isabel war Level Europäer These schwimmen. Verstehen Sie Spaß bei <UNK> aus Mallorca Heute und zwanzig Uhr fünfzehn im Ersten.
END|20190817150956|2019-08-17_1500_DE_DasErste_Tagesschau
```

**_Speech Transcript using Voice Activity Detection (VAD)_**

``` bash    
TOP|20190817150002|2019-08-17_1500_DE_DasErste_Tagesschau
COL|Communication Studies Archive, UCLA
UID|29979bf0-c101-11e9-a5ab-3bdd627efb4b
DUR|00:09:54
VID|720x576|640x512
SRC|Osnabruck, Germany
CMT|Afternoon news
CC1|DEU 150
ASR_02|DE
20190817150009.960|20190817150013.720|CC1|Hier ist das Erste Deutsche Fernsehen mit der tagesschau.
ASR_02|2019-08-22 12:37|Source_Program=Kaldi,infer-vad.sh|Source_Person=Aashish Agarwal|Codebook=Deutsch Speech to Text
20190817150014.280|20190817150058.770|ASR_02|Indem der Bohrungen im <UNK> ist es die erste deutsche Fernsehen mit der Tagesschau. Nein. Die im Studio Karolinen Kanzler Guten Tag meine Damen und Herren ich begrüße Sie zutage Schau. In Berlin findet oft hinter verschlossenen Türen statt an diesem Wochenende aber stehen viele Türen offen Politik wird dann zwar nicht gemacht aber die Bürger sind eingeladen sich über die Arbeit der Bundesregierung zu informieren das Kanzleramt die Ministerien und das Bundes Presseamt bieten mehr als acht Hundert Veranstaltungen an das Motto in diesem Jahr Hallo. Teak.
20190817150058.770000|20190817150113.920|ASR_02|Die Familienministerin ist heute mit den Kindern aufgestanden macht den Auftakt beim Tag der offenen Tür Demokratie Grundrechte das muss schon bei den kleinsten Thema sein Amt Kinder rechts Bus wissen Sie genau was sie von der Ministerin erwachten.
20190817150113.920000|20190817150202.010|ASR_02|Recht auf <UNK>. Nun gewaltfreie Erziehung. In können das Recht eine Ausbildung zu machen nun das Recht das jedes Kind zur Schule gehen kann wenn man Behinderungen hart und so dass man trotzdem gleichberechtigtes heranwachsen. Auch Religionen Kultur und Summers Heute spricht der Bürger die Politiker hören es zu Hallo Politik das Kanzleramt Lied ein und alle vierzehn Ministerien Lassen hinter die Kulissen schauen Andrang und Ausflüge auch in Europas größten danken den hat das Gesundheitsministerium aufstellen lassen die gesund. <UNK> des Bürgers ist wichtig Aufklärung tut Not und auch die im <UNK> Quoten und so kann wer will sich gleich noch impfen lassen ehe bekommt die zweite Masern Impfung.
20190817150202.010000|20190817150226.490|ASR_02|Alles für Jens Partner. Bürger fragen Politiker antworten der Finanzminister der auch ist Pedell Chef werden will lässt sich auch vom Volk wenig entlocken und nichts zur Pacht nach innen Wahl zur Demokratie dazu dass man sich auch mit <UNK> <UNK>. Gut spricht und Bambus sagt Wenn was zu sagen. Deutsche <UNK> also der Vizekanzler Morgen dann die Kanzlerin.
20190817150226.490000|20190817150331.890|ASR_02|In der C die EU wird über einen Parteiausschluss des früheren Verfassungsschutz Präsidenten Maßen diskutiert Die Vorsitzende Kramp Karrenbauer sagte den Zeitungen der Funke Mediengruppe sie sehe beimaßen keine Haltung die ihn mit der C die EU noch wirklich verbinde Allerdings gebe es hohe Hürden für einen Parteiausschluss Der sächsische Ministerpräsident Kretschmer Kreta. Die Überlegungen Man schließt er niemanden aus der C D U aus nur weil er unbequem sei maßen gilt als konservativer C die EU Politiker und Gegner von Merkels Flüchtlingspolitik. In Hongkong haben erneut tausende Menschen für Freiheit und Demokratie demonstriert Heute marschierten vorwiegend Lehrer zum Sitz der umstrittenen Regierungschefin Lärm der Protest verlief friedlich Unterdessen trafen sich in einem Park der Metropole Tausender Gegendemonstranten mit chinesischen Fahnen die sich selbst die <UNK>. Dieser Hongkongs nennen die Zentralregierung in Peking hatte zuletzt vor Unruhen gewarnt Einheiten der bewaffneten Volkspolizei sind seit Tagen in der der benachbarten chinesischen Staat Chengguan stark zunimmt.
20190817150331.890000|20190817150354.390|ASR_02|Im Sudan ist nach langen Verhandlungen der Weg für eine Übergangsregierung frei Vertreter von Opposition und bislang regierende Militär Rat haben heute in der Hauptstadt Khartum ein Abkommen unterzeichnet das einen gemeinsamen Rat von Zivilisten und Militärangehörigen vorsieht Dieser soll etwas mehr als drei Jahre lang regieren. Sollen Wahlen stattfinden.
20190817150354.390000|20190817150413.860|ASR_02|Der Sudan war eine britische Kolonie und wurde neun Hundert sechsundfünfzig unabhängig politisch stabile Phasen gab es seitdem kaum mehrmals putschte sich das Militär an die Macht neun Hundert neunundachtzig der Staatsstreich durch Generalleutnant Baschir der später offiziell Präsident wird unterstützt wird davon Islamisten.
20190817150413.860000|20190817150423.970|ASR_02|Unter ihrem Einfluss verhängte Baschir ein Scharia Gesetz und verschärfte damit den Konflikt mit dem Süden des Landes in dem das Christentum und traditioneller Religionen verbreitet sind.
20190817150423.970000|20190817150443.350|ASR_02|In Baschir 's Zeit fällt auch der Ausbruch des Darfur Konflikts Regierungstreue Milizen gehen brutal gegen rebellierende Volksgruppen vor ein Hundert Punkt null null null werden getötet der Konflikt ist bis heute nicht gelöst. <UNK> Internationale Strafgerichtshof verhängte Haftbefehle gegen Baschir unter anderem wegen Kriegsverbrechen und Völkermordes.
20190817150443.350000|20190817150446.440|ASR_02|<UNK> zwei Tausend elf wird der Südsudan unabhängig.
20190817150446.440000|20190817150452.650|ASR_02|In der Folge stürzt der Sudan in eine wirtschaftliche Krise die zuletzt in immer stärkere Proteste mündet.
20190817150452.650000|20190817150512.090|ASR_02|Dreißig Jahre nach seiner Machtübernahme wird bei schier aus den eigenen Reihen gestürzt die Kontrolle übernimmt ein Militärrat. <UNK> allen Landesteilen sind sie nach Khartum gereist um einen historischen Tag zu feiern. <UNK> Rad ist nun Geschichte Es beginnt eine neue Ära.
20190817150512.090000|20190817150531.260|ASR_02|De la Rey kann ich endlich wieder frei durch atmen alles war sehr teuer lieferbaren verzweifelt. Zwei Unterschriften festlicher Rahmen und viele Prominente aus dem Ausland. Der von Opposition und Militär besiedeln das über Monate mühsam verhandelte Vertrags.
20190817150531.260000|20190817150554.510|ASR_02|Der souveräner Rat ist künftig höchstes Staatsorgan Opposition und Militärs entsenden jeweils fünf Vertreter den elften bestimmen beide einvernehmlich ein General führt zunächst den Vorsitz. <UNK> überwacht die Regierungsbildung die Opposition benennt den Premierminister das Militär den Innen und Verteidigungsminister.
20190817150554.510000|20190817150557.720|ASR_02|Nach neununddreißig Monaten Gibt es Wahlen.
20190817150557.720000|20190817150633.030|ASR_02|Hagar militärische Gruppen sollen künftig der Armee unterstellt werden Sie haben Anfang Juni ein Protest kennt mit brutaler Gewalt aufgelöste Ska viele Tote eine schwere Bürde Nun soll ein neues Kapitel aufgeschlagen werden. Wir hoffen dass es mit dem Sudan jetzt aufwärts geht weder stolzer von Saldanha im können die Waffen niederlegen Frieden schließen können. <UNK> und <UNK>. Für Millionen ist ist der Tag der Freiheit auch wenn auf dem Weg zur Demokratie Unwägbarkeiten bleiben.
20190817150633.030000|20190817150656.460|ASR_02|Der Kult Film ehe sie wieder hat ihn berühmt gemacht das erste große Roadmovie der Kinogeschichte Eine begeistert gefeiert der Rebellion gegen das U es Establishment der späten sechzig er Jahrgang Peter Fonda wurde damit zum Idol der Hippiebewegung jetzt ist der Schauspieler im Alter von neunundsiebzig Jahren gestorben Nach Angaben seiner Familie. <UNK> er den Folgen einer Lungenkrebserkrankung.
20190817150656.460000|20190817150759.670|ASR_02|Als Easy Rider suchte er die Freiheit und fand. Trotz der NRO. Peter Fonda spielte an der Seite von Dennis Hopper fünfzig Jahren nicht nur eine Hauptrolle in Easy Rider Er schrieb auch am Drehbuch mit und produzierte. Abenteuer Film und Gesellschaftskritik zugleich brachte Easy Rider Peter Fonda seine erste Oscar Nominierung ein und machte ihm früher Leinwand Legende die Schauspielerei hatte er in den Genen schon sein Vater Henry Fonda war einst dar auch seine Schwester Jane reüssierte in Hollywood die Mutter hatte sich das Leben genommen als Peter und Jane auch Kinder. Vielleicht auch deshalb lagen Peter Fonda melancholische Räume. Ins Bienenzüchter Vietnam Veteranen kämpfte er in dem Film Julies Gold gegen Kriegs Trauma und Einsamkeit. Hat in den Vertrag ihre Einkäufe selbst. Ich mach das Schiff. Ich bin nur so durcheinander. Wenn man sich neuen Dingen gegenüber verhält.
20190817150759.670000|20190817150801.200|ASR_02|Neuen Gefühlen.
20190817150801.200000|20190817150802.490|ASR_02|Ein Menschen.
20190817150802.490000|20190817150834.050|ASR_02|Für diese Rolle gewann von da den Golden Globe siebenundzwanzig Jahren nach Easy Rider Kamm Becks wie diese sind selten in Hollywood. Es ist großartig zurück zu sein Jahresberichte Weber. Mit einem Stern auf dem Hollywood Bulevar wird er im Filmgeschäft unsterblich auch wenn er im Alter von neunundsiebzig Jahren den Kampf gegen den Lungenkrebs verliert seine Schwester Jane Fonda veröffentlichte eine Stellungnahme in seinen letzten Tagen hatte ich eine schöne Zeit mit ihm allein erging lachend davon.
20190817150834.050000|20190817150846.620|ASR_02|Die Wette Aussichten Morgen wechselnd bewölkt mit sonnigen Abschnitten später vom Südwesten bis in die Mitte Schauer Zum Teil Gewitter die sich Richtung Osten ausbreiten achtzehn bis dreiunddreißig Grad.
20190817150846.620000|20190817150931.800|ASR_02|Die Tagesschau meldet sich wieder um siebzehn Uhr fünfzig Ich wünsche Ihnen einen schönen Tag. Neben Vorlage oder die Sängerin der Banco Bena bei Vala Gong gab. Verstehe gackerte wahrlich Das ist Hauptsache wirklich verstehen war. Der Rhein auf dem Tappert Fella aller Verstehen Sie Spaß Marc Forster schmeißen Gepard. Von den ehrlich Brothers ist nur einer ehrlich. Abel. Isabel war Level Europäer These schwimmen. Verstehen Sie Spaß Spezial aus Mallorca heute um zwanzig Uhr fünfzehn im Ersten.
20190817150931.800000|20190817150955.080|ASR_02|<UNK>.
END|20190817150956|2019-08-17_1500_DE_DasErste_Tagesschau
```

### Future Work

1. As Red Hen's transcribes News. It would be interesting to train the model with News data and check for the improvements in the result.

2.  Also, Dan Povey (Kaldi’s Architect) has suggested using BPE (Byte Pair Encoding) for Acoustic and Language Modelling. Thus, essentially relying on graphemes and not on the lexicon to solve the Homonyms, Morphology and Plural challenges.

This ends my 13 weeks journey at [Red Hen Lab](http://www.redhenlab.org/home) for GSoC-2019. I enjoyed working with the team, and I learned a lot solving the challenges. I want to specially thanks to my mentor Dr. Jan Gorisch, for providing valuable comments and guiding me over my journey!

And most importantly, I express my gratitude to the people behind the Google Summer of Code. I had a very enjoyable experience working in GSoC 2019. I hope I keep contributing.

### Others

- [My GSoC 2019 Journey](https://aashishag.github.io/categories/#gsoc)
- [Repository of Code](https://github.com/AASHISHAG/asr-german)