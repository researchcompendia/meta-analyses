Reproducing bicycle helmet research
===================================
**Tim Churches**  
Sydney, Australia  
tim∙churches@gmail∙com  
16 June 2013.

About this document
-------------------
This document contains reproductions of aspects of published research into bicycle helmets. The intent of reproducing such research is to check its accuracy and correctness, and in the cases where the research has made selective use of available data, to re-present that research using all the data available from the source(s) used at the time it was done.

This document is also an example of [literate programming](http://en.wikipedia.org/wiki/Literate_programming), in which expository text is interleaved with computer program code and the output of that code. The document was created in markdown format using [RStudio](http://www.rstudio.com) and the [_knitr_](http://yihui.name/knitr/) package for the [R statistical environment](http://www.r-project.org). The source file for this document, which includes all the programme code required to create the output shown, as well as the data used by that programme code, are all freely available on [GitHub](https://github.com/timchurches/meta-analyses/blob/master/benefits-of-reproducible-research/reproducing-bicycle-helmet-research.Rmd) under the terms of the [Creative Commons Attribution-ShareAlike 3.0 Australia license](http://http://creativecommons.org/licenses/by-sa/3.0/au/). Copyright and licensing arrangement of external images and other content included in this document by hyperlink are indicated in the text adjacent to each piece of external content. 

Graph from a poster presentation by Colin F. Clarke presented at the Velo-city 2007 international cycling conference
--------------------------------------------------------------------------------------------------------------------
The source is a poster presentation at the international [Velo-city conference held in Munich in 2007](http://www.nationaler-radverkehrsplan.de/eu-bund-laender/eu/velocity/schedule.phtml). The reference is:
> Colin Clarke (United Kingdom) - Cyclists' Touring Club: The Case against Bicycle Helmets and Legislation (poster). Velo-city 2007 ([PDF of paper](http://www.nationaler-radverkehrsplan.de/eu-bund-laender/eu/velocity/presentations/velocity2007_pp_17c_long_public.pdf)). 

The first paragraph in the section of the paper titled _Bicycle helmet legislation_ states (verbatim):
> Australia led the way in 1990 with bicycle helmet legislation in the state of Victoria. Police enforced the law and the number of people cycling immediately dropped. A reported 36% drop in number of cyclists (Finch, Heiman, Nelger) from 3121 to 2011 was from surveys in Melbourne, where 42% wore helmets before the law. The drop of 36% (see Fig 1) represents more than half of those (58%) not wearing helmets. 

The figure mentioned is this (the figure is also [available in Wikimedia Commons](http://en.wikipedia.org/wiki/File:36%25_reduction_in_cycling_Melbourne.jpg) under a Creative Common license):
![Figure by Colin Clarke from 2007 Velo-city poster](http://upload.wikimedia.org/wikipedia/commons/thumb/3/35/36%25_reduction_in_cycling_Melbourne.jpg/800px-36%25_reduction_in_cycling_Melbourne.jpg)

As noted by Clarke, the source of these data is a 1993 Monash University Accident Research Centre (MUARC) report by Finch _et al_. ([PDF of report](http://www.monash.edu.au/miri/research/reports/muarc045.pdf)). The first step is to abstract the available data from the report. The report contains data from four surveys of cyclists in Melbourne: the first at 105 sites conducted in December 1987 and January 1988, the second at a subset of 80 of the original 105 sites, in May-June 1990, and two more surveys at a subset of 64 of the 80 sites, in May-June 1991 and 1992. The report contains detailed data restricted to the common 64 sites in Melbourne for the May-June surveys in 1990, 1991 and 1992. These are the data used by Clarke (or at least the first two of these three years of comparable data) and thus are the data we will focus on here. 

The mandatory helmet law came into effect in Victoria in July 1990, thus there is one pre-law and two post-law data points in this subset of the 64 observation sites common to all three years 1990 to 1992.  From Section 5.2.2 of the report (page 18), we can obtain the percentage of road cyclists observed to be wearing helmets for each of three age groups (5 to 11 year olds, 12 to 17 year olds, and those aged 18 or older, the age group of each cyclist estimated by the survey observers) in each of the three years 1990 to 1992. From figures 10 to 12 on pages 20-21 of the report we can obtain the age-group-specific total counts of cyclists (shown as "n=" in the figures). Summing the counts from figures 10 to 12 gives yearly totals which agree precisely or to within less than 0.1% of the total counts for each year given in section 5.6.4 on page 35, indicating that our data are correct and complete (presumably the small and ignorable discrepencies are due to missing age group information in a handful of observations).

First, we create a data frame in R containing these data, and calculate the count of cyclists wearing and not wearing helmets in each age group in each year:





```r
finch <- data.frame(age.group = ordered(c(rep("5-11", 3), rep("12-17", 3), rep("18+", 
    3)), levels = c("5-11", "12-17", "18+")), year = factor(c(1990, 1991, 1992)), 
    percent.helmeted = c(65, 78, 77, 21, 45, 59, 36, 74, 84), cyclists.counted = c(259, 
        235, 281, 1293, 670, 713, 1567, 1106, 1483))
finch$cyclists.helmeted <- with(finch, percent.helmeted * cyclists.counted/100)
finch$cyclists.unhelmeted <- with(finch, (100 - percent.helmeted) * cyclists.counted/100)
```


The data look like this:
<!-- html table generated in R 3.0.2 by xtable 1.7-1 package -->
<!-- Thu Feb 20 13:04:28 2014 -->
<TABLE border=1>
<TR> <TH> age.group </TH> <TH> year </TH> <TH> percent.helmeted </TH> <TH> cyclists.counted </TH> <TH> cyclists.helmeted </TH> <TH> cyclists.unhelmeted </TH>  </TR>
  <TR> <TD> 5-11 </TD> <TD> 1990 </TD> <TD align="right"> 65 </TD> <TD align="right"> 259 </TD> <TD align="right"> 168 </TD> <TD align="right"> 91 </TD> </TR>
  <TR> <TD> 5-11 </TD> <TD> 1991 </TD> <TD align="right"> 78 </TD> <TD align="right"> 235 </TD> <TD align="right"> 183 </TD> <TD align="right"> 52 </TD> </TR>
  <TR> <TD> 5-11 </TD> <TD> 1992 </TD> <TD align="right"> 77 </TD> <TD align="right"> 281 </TD> <TD align="right"> 216 </TD> <TD align="right"> 65 </TD> </TR>
  <TR> <TD> 12-17 </TD> <TD> 1990 </TD> <TD align="right"> 21 </TD> <TD align="right"> 1293 </TD> <TD align="right"> 272 </TD> <TD align="right"> 1021 </TD> </TR>
  <TR> <TD> 12-17 </TD> <TD> 1991 </TD> <TD align="right"> 45 </TD> <TD align="right"> 670 </TD> <TD align="right"> 302 </TD> <TD align="right"> 368 </TD> </TR>
  <TR> <TD> 12-17 </TD> <TD> 1992 </TD> <TD align="right"> 59 </TD> <TD align="right"> 713 </TD> <TD align="right"> 421 </TD> <TD align="right"> 292 </TD> </TR>
  <TR> <TD> 18+ </TD> <TD> 1990 </TD> <TD align="right"> 36 </TD> <TD align="right"> 1567 </TD> <TD align="right"> 564 </TD> <TD align="right"> 1003 </TD> </TR>
  <TR> <TD> 18+ </TD> <TD> 1991 </TD> <TD align="right"> 74 </TD> <TD align="right"> 1106 </TD> <TD align="right"> 818 </TD> <TD align="right"> 288 </TD> </TR>
  <TR> <TD> 18+ </TD> <TD> 1992 </TD> <TD align="right"> 84 </TD> <TD align="right"> 1483 </TD> <TD align="right"> 1246 </TD> <TD align="right"> 237 </TD> </TR>
   </TABLE>


From that, we can calculate the percentage of helmeted cyclists in May-June 1990: 100*(168+272+564)/(259+1293+1567) = 32.1898%. This is rather different from the 42% given by Clarke as the percentage cycling with helmets pre-law in the quoted paragraph above. However, the proportion of pre-law helmeted cyclists shown in his graph is approximately 32%, so it may be just a typo in the paper.

So let's reproduce the graph, but using all three years of data, and showing each age group as well as all age groups combined (note that we need to transform the dataset into a long, thin layout first using the handy `melt()` function in the `reshape2` library):


```r
finchm <- melt(finch, id = c("age.group", "year"), measure.vars = c("cyclists.helmeted", 
    "cyclists.unhelmeted"), variable.name = "helmeted", value.name = "count")
finchm$helmeted <- ordered(finchm$helmeted, levels = c("cyclists.helmeted", 
    "cyclists.unhelmeted"), labels = c("Wearing helmet", "Not wearing helmet"))
ggplot(finchm, aes(x = year, y = count, fill = helmeted)) + geom_bar(stat = "identity") + 
    facet_grid(. ~ age.group, margins = T, labeller = label_both) + scale_fill_brewer(type = "qual", 
    name = "") + labs(x = "Year of survey", y = "Count of cyclists observed", 
    title = "Cyclist counts and helmet wearing in Melbourne, May-June 1990 to May-June 1992\n(Mandatory helmet laws introduced July 1990.)\nSource: Finch et al. Monash University Accident Research Centre Report No. 45, 1993") + 
    theme_bw()
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 

### Comment
The first two bars in the rightmost panel in the graph above correspond to the two bars in the graph in the Clarke paper. However, this graph shows all of the relevant, comparable data that is available in the Finch _et al_. report. It provides a much fuller picture than the selective use of data in the Clarke graph.

### Postscript
Colin Clarke has communicated that the 42% figure in his paper comes from another reference in the paper, even though it is not attributed to it, and is therefore not a typo. Readers can be forgiven for assuming that the figure is derived from the Finch _et al_. report, I feel. He has also communicated that he did not use the 1992 data available in the report in his graph because a bicycle rally passed through one of the observation points. Here is what Finch _et al_. had to say on this issue (p44 of their report):

> Another explanation for some of the increase in bicyclist numbers in 1992 is related to the fact that there appears to have been a bicycle rally passing through one of the sites (site 80, in 1991/2, Appendix 2) on a Sunday morning. This particular site is a popular recreational area and is part of a defined bicycle track. In 1991, it was rainy during all observations of this site and very few bicyclists were observed. Although the weather was generally fine in 1990, the number of bicyclists in 1992 in this area was still more than would have been expected on the basis of pre-law levels. The chance occurrence of a large group of bicyclists passing through a particular area is one of the hazards of observational surveys such as these. From a statistical point of view, however, an occurrence such as this is a true observation, well within the bounds of “normal” behaviour for that time period, and cannot be excluded from the analysis.
> 
> The chance occurrence of events such as different weather conditions or large groups of bicyclists, as described above, can be a problem associated with observational surveys even though observation sessions are randomly allocated within time and space strata. Such problems can be overcome, or minimised, by conducting larger surveys. Analysis methods, however, cannot overcome such problems (eg. by focussing on “fine” sites only) because it upsets the matched 64 site comparison of 1990 versus 1991.
> 
> The importance of the analysis of the total numbers of bicyclists as a measure of exposure trends is that it enables an assessment of trends in adults because, unlike timed-exposure, this information was available in 1990, prior to the law. This means that to have a valid comparison of pre- and post- law levels in adults, we have no choice but to look at the number of bicyclists over time. On the other hand, comparisons of the numbers of bicyclists leads only to valid conclusions about the 64 observation sites in common to each of the MUARC surveys. Unlike the timed exposure data, these results cannot, and should not, be extrapolated to the whole of metropolitan Melbourne; they only describe the 64 sampled sites.

Readers can form their own opinions about whether such second-guessing of the authors' intentions represents unjustified selectivity in the use of the available data, or not.

---

This document will be extended to incorporate more reproductions in the future.




