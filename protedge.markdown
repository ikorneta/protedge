---
title: "Visualisations of Operation Protective Edge"
author: "Iga Korneta"
date: "Wednesday, August 13, 2014"
output: html_document
status: publish
---
 
### Introduction
 
I first became interested in visualising [Operation Protective Edge](https://en.wikipedia.org/wiki/Operation_Protective_Edge) when I saw the huge lists of victims on the [IMEMC](http://www.imemc.org/article/68429) and [Al-Akhbar blog/journal](http://english.al-akhbar.com/node/20528) websites. I wanted to create some sort of a visual shorthand of the operation, beyond lists and statistics.
 
This document shows some of the results of my curiosity.
 
 
### Data sources and processing
 
#### Sources
 
I scraped the data from [IMEMC](http://www.imemc.org/article/68429), [Al-Akhbar](http://english.al-akhbar.com/node/20528) and, for the Israeli soldier fatalities, [Times of Israel](http://www.timesofisrael.com/fallen-idf-soldiers-in-operation-protective-edge/). Unfortunately, it turned out that the data was rather dirty, and thus required a lot of (irreproducible, unless you want to devote a lot of time to that) manual massaging. 
 
In particular:
 
* IMEMC and Al-Akhbar use different Arabic-to-English transliterations;
 
* IMEMC only lists identified victims, Al-Akhbar lists all;
 
* multiple records differ on ages, locations etc. between the sources; some records are obviously repeated in both sources, with minor spelling errors etc..
 
My chosen procedure was common-sense and as follows:
 
* match mutually identified records where possible;
 
* match identified IMEMC records with "unknown" placeholder records from Al-Akhbar from the same date where possible;
 
* add placeholder records to the Al-Akhbar list as needed. Those placeholder records are identified as having post-decimal points digits. So, for example, "unknown1" is an original Al-Akhbar placeholder record, "unknown1.1" was added to facilitate list merging.
 
Because I chose a greedy procedure for merging, the list is slightly longer than the 'official' statistics. At the time of the data processing (Aug 12, 2014), the raw Al-Akhbar file has 1940 records. The final file has 2019 Palestinian records (in addition to 64 Israeli ones). 1102 of the Palestinian records repeat between the Al-Akhbar and IMEMC lists.
 
#### Processing
 
The final file contains the following variables:
 
* date, ordinal day (starting from July 8th, 2014 as the first day of the operation), ethnicity;
 
* full name, first name, last name, name summary, age, sex, place of death, circumstances from the Al-Akhbar file;
 
Gender data was derived by running the first names through [here](http://www.indiachildnames.com/genderof.aspx) and [here](http://www.gpeters.com/names/baby-names.php).
 
Name summary is a numerical shorthand for name, defined as ((ord(last_name_low[0])-96)*10+(ord(last_name_low[1])-96)), where ord(x)=ASCII value of x. (ord(a)-96)=1
 
* full name, name summary, age, sex, place of death, circumstances from the IMEMC file - column names starting from (IMEMC_);
 
* combined-record name summary, age, sex, and place of death; IMEMC records, which are supposed to be more correct, take precedence over Al-Akhbar records;
 
* age group, defined as: "Unknown", "Child" (<=14), "Young adult" (<=24), "Adult" (<=54), "Elderly";
 
* simulated ages and name summaries, for the plots where I wanted to add the "unidentified" records.
 
 
### Results
 
#### Exploratory analysis
 
Exploratory graphs show enrichment in the young male category:
 
<img src="/images/figure/explot1.png" title="plot of chunk explot1" alt="plot of chunk explot1" style="display: block; margin: auto;" />
 
Side by side comparison of victim age stratification vs. the age stratification of the Gaza Strip (data from [Index Mundi](http://www.indexmundi.com/gaza_strip/demographics_profile.html)):
 
<img src="/images/figure/explot2.png" title="plot of chunk explot2" alt="plot of chunk explot2" style="display: block; margin: auto;" />
 
Interestingly, a chi-square test shows a p-value of 0.2133, which would indicate that these two distributions are **not** markedly different (despite looking different on the barplots above).
 
#### Victims by day of operation and Information updating
 
This plot show the cumulative deaths by day of operation:
 
<img src="/images/figure/explot3.png" title="plot of chunk explot3" alt="plot of chunk explot3" style="display: block; margin: auto;" />
 
The "unknown" category will be pushed forward the more and more information there arrives. The Al-Akhbar website is not back-updated for new information regarding previously unidentified victims - thus freezing the initial status of the information.
 
<img src="/images/figure/explot4.png" title="plot of chunk explot4" alt="plot of chunk explot4" style="display: block; margin: auto;" />
 
#### Final visualisations: the Hexbin and the Scatterplot
 
The goal of visual analytics is to bring order to chaos. Nevertheless, I was rather concerned about the ethics of doing so when it comes to summarising human deaths. It makes them too clean; too sterile. I wanted a visualisation that would show me the chaos - that would not shirk from it.
 
 
I started from a hexbin plot.
 

    ## Warning: Removed 789 rows containing missing values (stat_hexbin).
    ## Warning: Removed 789 rows containing missing values (stat_smooth).

<img src="/images/figure/explot5.png" title="plot of chunk explot5" alt="plot of chunk explot5" style="display: block; margin: auto;" />
 
I added simulated age data to account for the yet-unidentified victims.
 
<img src="/images/figure/explot6.png" title="plot of chunk explot6" alt="plot of chunk explot6" style="display: block; margin: auto;" />
 
Then, I decided to abandon all pretense of a structure and use a scatterplot instead.
 
<img src="/images/figure/explot7.png" title="plot of chunk explot7" alt="plot of chunk explot7" style="display: block; margin: auto;" />
 
(Men are coded dark red; women, black; the colour is meant to be unpleasant and evocative of blood splatter.) From the chaos, another sort of order emerges as the death clusters determine the pivotal points of the operation. It is now perfectly clear when the ground invasion started (07/20) and when the ceasefires occurred.
 
 
It's possible to add the information about Israeli soldiers here:
 
<img src="/images/figure/explot8.png" title="plot of chunk explot8" alt="plot of chunk explot8" style="display: block; margin: auto;" />
 
But it's not really obligatory.
