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


![](
/others/speech-recognition-pipeline-3.png)

``` bash
$ ./run-server.sh
$ ./run-worker.sh
$ ./model-run.slurm specify_the_number_of_days_from_the_current_date_the_model_should_transcribe
``` 

This is a small excerpt from the Red Hen News Dataset. The MP4 files are programmatically converted to WAV and fed to Kaldi-Gstreamer-Server. The model output, i.e., the transcripts are further formatted to adopt [Red Hen's Data Format](https://sites.google.com/site/distributedlittleredhen/home/the-cognitive-core-research-topics-in-red-hen/red-hen-data-format#TOC-Audio-Pipeline-Tags).
    
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
END|20190817150956|2019-08-17_1500_DE_DasErste_Tagesschau```

This ends my 13 weeks journey at [Red Hen Lab](http://www.redhenlab.org/home) for GSoC-2019. I enjoyed working with the team, and I learned a lot solving the challenges. I want to specially thanks to my mentor Dr. Jan Gorisch for providing valuable comments and guiding me over my journey!

And most importantly, I express my gratitude to the people behind Google Summer of Code. I had a very enjoyable experience working in GSoC 2019. I hope I keep contributing.

### Others

- [My GSoC 2019 Journey](https://aashishag.github.io/categories/#gsoc)
- [Repository of Code](https://github.com/AASHISHAG/asr-german)