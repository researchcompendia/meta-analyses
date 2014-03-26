The benefits of reproducible research: a public health example
==============================================================
**Tim Churches**  
Sydney, Australia  
tim∙churches@gmail∙com  
9 March 2013.

Updated 20 February 2014 - see Postscript.

About this document
-------------------
This document is an example of [literate programming](http://en.wikipedia.org/wiki/Literate_programming), in which expository text is interleaved with computer program code and the output of that code. The document was created in markdown format using [RStudio](http://www.rstudio.com) and the [_knitr_](http://yihui.name/knitr/) package for the [R statistical environment](http://www.r-project.org). The source file for this document, which includes all the programme code required to create the output shown, as well as the data files read by that programme code, are all freely available on [GitHub](https://github.com/timchurches/meta-analyses/tree/master/benefits-of-reproducible-research) under the terms of the [Creative Commons Attribution-ShareAlike 3.0 Australia license](http://http://creativecommons.org/licenses/by-sa/3.0/au/), with the exception of the link to the figure from the journal _Accident Analysis and Prevention_, which is copyright Elsevier Pty Ltd. 

Pre-amble
---------
Recognition of the benefits of [reproducible research](http://en.wikipedia.org/wiki/Reproducibility#Reproducible_research) has been growing in many scientific disciplines over the last decade, including [epidemiologic research](http://aje.oxfordjournals.org/content/163/9/783.full) and [biostatistics](http://biostatistics.oxfordjournals.org/content/10/3/405.full), both of which are foundation stones of public health. The aim of this article is to provide an example of the benefits of replication of reproducible public health research, and to itself serve as an illustration of methods for publishing research which make its replication, and possibly extension, as fast and efficient as possible.

The example concerns a 2011 meta-analysis of bicycle helmet effectiveness by Rune Elvik ([Elvik 2011a]), published in the well-regarded journal _Accident Analysis & Prevention_, of which Professor Elvik is also one of two editors-in-chief. As the title of Elvik's meta-analysis suggests, it was itself a re-analysis and extension of a 2001 meta-analysis by Attewell _et al_. ([Attewell 2001]). The Elvik meta-analysis has attracted considerable attention because it suggests that bicycle helmets may not be as effective in preventing injuries in the event of an accident as had previously been thought. As at March 2013, it has been referenced by 15 other papers according to [Scopus](http://www.scopus.com/results/citedbyresults.url?sort=plf-f&cite=2-s2.0-79952449461&src=s&imp=t&sid=12CBF6348C488B4C46AC2785C1C17A17.iqs8TDG0Wy6BURhzD3nFA%3a30&sot=cite&sdt=a&sl=0&origin=inward&txGid=12CBF6348C488B4C46AC2785C1C17A17.iqs8TDG0Wy6BURhzD3nFA%3a2). The paper has also been cited extensively in (often acrimonious) public discourse over bicycle helmets and whether the wearing of them should be promoted and/or mandated. It is quite possible that the Elvik meta-analysis has influenced public policy formation in jurisdictions that are currently considering bicycle helmet initiatives. Thus, the Elvik meta-analysis is a paper with real-world impact (pun intended).

Problems with publication bias adjustment
-----------------------------------------
Although I had glanced through the Elvik paper when it appeared in early 2011, it wasn't until September 2012 that I read it in detail. Elvik employed the trim-and-fill method as developed by Duval and Tweedie ([Duval & Tweedie 2000]) to adjust for potential [publication bias](http://en.wikipedia.org/wiki/Publication_bias). For a strict empiricist, the trim-and-fill method is a bit alarming, because it requires the "invention" of hypothetical unpublished studies. In a nutshell, the method involves the use of a signed rank test to estimate the number of outlier study results which need to be trimmed from the funnel plot in order to make it as close to symmetrical as possible, followed by recalculation of the summary effect measure (odds ratio in this case) after the outliers have been temporarily set aside (trimmed). This trimming and recalculation  procedure is repeated until a stable summary OR is obtained. The trimmed outlier study results are then restored to the funnel plot, and a set of hypothetical unpublished studies are added to the funnel plot as  mirror images of the previously trimmed outlier studies, in order to achieve symmetry. The key point is that  the vertical axis of symmetry around which the hypothesised studies (which are supposed to exist but to have never seen the light of day) should be added is the re-estimated summary effect measure after trimming. I am not going to discuss here the range of views on this and other methods for correcting hypothetical publication bias, nor the advisability of applying this adjustment technique to these particular bicycle helmet effectiveness studies, nor the advisability of applying the method, as Elvik has done, to pooled studies with different outcome measures (head, face and neck injuries, on each of which helmets clearly have different effects). It suffices to say that if the trim-and-fill technique is to be applied at all, then it should be applied correctly.

I noticed that figures 1 and 4 in the Elvik 2011 paper didn't look right: the hypothetical mirror-image "fill" studies had been added around a vertical axis of symmetry located at log(OR)=0 (i.e. OR=1), instead of around an axis of symmetry located at the weighted mean of the pooled results (after outliers have been trimmed), which in the case of bicycle helmets and head injuries, is considerable less than OR=1. The result of such an error is an over-adjustment of the summary odds-ratio, making bicycle helmets appear less effective than they really are. 

Given these apparent errors in the figures, I thought it best to attempt to replicate the entire Elvik meta-analysis. The raw count data used in the Attewell _et al_. meta-analysis were conveniently available in an appendix to a monograph on the study ([Attewell 2000]), and these data were entered into a data file. Elvik had added the results of four more studies. Results were easily abstracted from the published paper for one of these four studies. Unfortunately the published versions of two of the studies did not include count data, as is usually required for meta-analysis, and instead only provided adjusted ORs with confidence limits. The fourth paper apparently included count data but these were missing from the only copy I was able to obtain electronically. 

Due to these difficulties, I wrote to Professor Elvik in late September 2012 requesting a copy of the data that he had used from these four studies. To his immense credit, Professor Elvik responded promptly, sending me a spreadsheet which contained all the data as well as all the calculations for his meta-analysis. I was a bit surprised to learn that he was using a spreadsheet to undertake meta-analysis, given that very capable and well-tested meta-analysis packages are available for Stata, R, SAS and other statistical software. The first thing I noticed in the spreadsheet were differences in the count data for three of the studies from the Attewell _et al_. meta-analysis. I went back to the original papers for those studies and found that the Attewell _et al_. data were correct but had apparently been transcribed incorrectly into the spreadsheet. These errors were relatively minor and did not materially affect the results, but nonetheless the data Elvik had used in his calculations were slightly wrong. However, I was able to obtain from the spreadsheet the counts for one of the new studies, and to determine that Elvik had estimated the variance of the adjusted odds ratios of the other two studies using the 95% confidence limits. This is not an unreasonable approach in the absence of the raw count data, although the raw counts might have been obtainable by contacting the authors of those studies. The spreadsheet also provided the precise continuity adjustments which Elvik had used for a few studies which included zero counts (Attewell _et al_. had excluded these studies).




It was then very straightforward to replicate the meta-analysis, including the trim-and-fill publication bias adjustment, using the [_meta_](http://cran.r-project.org/web/packages/meta/index.html) package for R. The R code which loads the data into a data frame named _**studies**_ is in the markdown source file for this document, but won't be shown here. First we will repeat the meta-analysis for the head injury outcome studies from Attewell _et al_ and examine the results.


```r
head.attewell <- studies[which(studies$injury.type == "head" & studies$meta.analysis == 
    "A"), ]
head.attewell.meta <- metagen(TE = yi, seTE = sei, studlab = study.label, data = head.attewell, 
    method.bias = "rank", label.e = "Injured", label.c = "Not injured", sm = "OR")
summary(head.attewell.meta)
```

```
## Number of studies combined: k=13
## 
##                         OR         95%-CI       z  p.value
## Fixed effect model   0.418 [0.373; 0.468] -15.109 < 0.0001
## Random effects model 0.386 [0.281; 0.531]  -5.847 < 0.0001
## 
## Quantifying heterogeneity:
## tau^2 = 0.1915; H = 2.14 [1.64; 2.78]; I^2 = 78.1% [63%; 87.1%]
## 
## Test of heterogeneity:
##      Q d.f.  p.value
##  54.85   12 < 0.0001
## 
## Details on meta-analytical method:
## - Inverse variance method
## - DerSimonian-Laird estimator for tau^2
```

Those results exactly match those given in Table 1 of the Elvik 2011 paper. Now we will do the trim-and-fill adjustment:

```r
head.attewell.tf <- trimfill(head.attewell.meta)
summary(head.attewell.tf)
```

```
## Number of studies combined: k=16 (with 3 added studies)
## 
##                        OR         95%-CI      z  p.value
## Random effects model 0.43 [0.309; 0.597] -5.023 < 0.0001
## 
## Quantifying heterogeneity:
## tau^2 = 0.2253; H = 2.1 [1.65; 2.66]; I^2 = 77.3% [63.4%; 85.9%]
## 
## Test of heterogeneity:
##      Q d.f.  p.value
##  66.02   15 < 0.0001
## 
## Details on meta-analytical method:
## - Inverse variance method
## - DerSimonian-Laird estimator for tau^2
## - Trim-and-fill method to adjust for funnel plot asymmetry
```

Unfortunately those results are different from the corresponding results given in Table 1 of the Elvik paper. Finally, let's examine a funnel plot (using the funnel() function from the _metafor_ package; the "filled" hypothetical studies are shown as empty squares):



```r
headmf <- rma(yi, vi, data = head.attewell, method = "FE")
headmf.tf <- trimfill(headmf)
funnel(headmf.tf, xlim = c(-6, 6), ylim = c(2, 0), steps = 11, xlab = xlabel, 
    ylab = ylabel, main = title, pch = 18, pch.fill = 22)
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-5.png) 



Compare that with Figure 1 from the Elvik 2011 paper:

![Fig 1 from Elvik 2011](http://ars.els-cdn.com/content/image/1-s2.0-S000145751100008X-gr1.jpg)

The overall pattern of points for the published studies are identical in both of the figures above (well, almost identical, due to the minor data errors underlying the Elvik figure), but the hypothetical "fill" study results are clearly in the wrong places in the Elvik figure.

After repeating this replication of the trim-and-fill procedure for each of the different types of injury outcome, it became clear that these errors were not confined to just these figures, but also affected all the publication bias adjustment results throughout the paper. Elvik based the conclusions of his study on these publication bias-adjusted results, and thus the correctness of the entire paper appeared to be in serious doubt.

In early October 2012, I wrote to Professor Elvik in his capacity as author of the paper, and to Dr Karl Kim, in his capacity as co-editor of _Accident Analysis & Prevention_, alerting them to these problems (incorrect data and incorrect bias adjustment calculations), providing an earlier version of the data files and R code used in this document as supporting evidence. I suggested that the entire paper ought to be retracted, in accordance with [COPE guidelines](http://publicationethics.org/files/retraction%20guidelines.pdf).

In late December 2012, _Accident Analysis & Prevention_ published a whole-of-paper corrigendum for the 2011 Elvik meta-analysis ([Elvik 2012c]). This nine-page corrigendum was itself unusual, because it included not just corrected results, but also a substantial amount of new material which did not appear in the seven-page original paper.

Other meta-analysis papers by Elvik
-----------------------------------
It appears that three other published papers of which Elvik was the sole author or a co-author are also affected by errors in the way trim-and-fill publication bias adjustments have been performed ([Høye & Elvik 2010], [Elvik 2011b], [Elvik 2012a]).The authors of the papers and editors of the journals were all alerted to these errors shortly after they were discovered in October 2012. At the time of writing, one of these papers has been withdrawn by the journal in which it was published ([Elvik 2012a]). There is one other paper by Elvik which relies on incorrect results from the 2011 bicycle helmet meta-analysis which will also need to be corrected ([Elvik 2012b]).

But the story doesn't end there.

Problems with the corrigendum
-----------------------------
Given the problems with the 2011 meta-analysis, I thought it wise to try to replicate all the results in the corrigendum. This was easily done using the raw study data I had previously assembled. First I abstracted the fixed-effects and random-effects summary results from Table 4 of the corrigendum into a data file, to permit convenient comparisons with the results of my replication. This was loaded as a data frame named **_results_**. The following code was used to attempt to replicate the table 4 results:



```r
# Calculate summary estimates for each group of studies as per Elvik 2012
# corrigendum table 4.  Note that metagen() uses DerSimonian-Laird pooling
# as default, and we specify the rank method as used by Elvik as the bias
# detection algorithm
subset.meta <- function(studies, injury.type, studies.included) {
    # Note: A=Attewell (old studies), E=Elvik (new studies)
    if (studies.included == "old") {
        meta.analysis <- c("A")
    }
    if (studies.included == "new") {
        meta.analysis <- c("E")
    }
    if (studies.included == "all") {
        meta.analysis <- c("A", "E")
    }
    injury.type.string <- paste(injury.type, collapse = "/")
    dfsubset <- studies[which(studies$injury.type %in% injury.type & studies$meta.analysis %in% 
        meta.analysis), ]
    ma <- metagen(TE = yi, seTE = sei, studlab = study.label, data = dfsubset, 
        method.bias = "rank", label.e = "Injured", label.c = "Not injured", 
        sm = "OR")
    subset.ma.results <- data.frame(source = "replica", injury.type = injury.type.string, 
        studies.included = studies.included, num.studies = ma$k, FE.OR = exp(ma$TE.fixed), 
        FE.LL95 = exp(ma$lower.fixed), FE.UL95 = exp(ma$upper.fixed), RE.OR = exp(ma$TE.random), 
        RE.LL95 = exp(ma$lower.random), RE.UL95 = exp(ma$upper.random))
    # print(summary(ma))
    return(rbind(results, subset.ma.results))
}
# Iterate through injury outcome types and old, new and all studies.
for (injtype in list(c("head"), c("face"), c("neck"), c("head", "face", "neck"))) {
    for (studies.incl in list("old", "new", "all")) {
        results <- subset.meta(studies, injtype, studies.incl)
    }
}
```

After sorting the results, we can examine them for discrepancies.



```r
print(xtable(results[, c(1, 2, 3, 4, 5, 11, 8, 12)], digits = 2), type = "html", 
    include.rownames = F)
```

<!-- html table generated in R 3.0.2 by xtable 1.7-1 package -->
<!-- Thu Feb 20 13:20:45 2014 -->
<TABLE border=1>
<TR> <TH> Source </TH> <TH> Injury Type </TH> <TH> Studies </TH> <TH> n </TH> <TH> Fixed-effects OR </TH> <TH> (FE 95% CI) </TH> <TH> Random-effects OR </TH> <TH> (RE 95% CI) </TH>  </TR>
  <TR> <TD> Elvik </TD> <TD> head </TD> <TD> old </TD> <TD align="right">  13 </TD> <TD align="right"> 0.42 </TD> <TD> (0.37-0.47) </TD> <TD align="right"> 0.38 </TD> <TD> (0.28-0.53) </TD> </TR>
  <TR> <TD> replica </TD> <TD> head </TD> <TD> old </TD> <TD align="right">  13 </TD> <TD align="right"> 0.42 </TD> <TD> (0.37-0.47) </TD> <TD align="right"> 0.39 </TD> <TD> (0.28-0.53) </TD> </TR>
  <TR> <TD> Elvik </TD> <TD> head </TD> <TD> new </TD> <TD align="right">   5 </TD> <TD align="right"> 0.71 </TD> <TD> (0.62-0.82) </TD> <TD align="right"> 0.58 </TD> <TD> (0.41-0.84) </TD> </TR>
  <TR> <TD> replica </TD> <TD> head </TD> <TD> new </TD> <TD align="right">   5 </TD> <TD align="right"> 0.71 </TD> <TD> (0.62-0.82) </TD> <TD align="right"> 0.58 </TD> <TD> (0.41-0.84) </TD> </TR>
  <TR> <TD> Elvik </TD> <TD> head </TD> <TD> all </TD> <TD align="right">  18 </TD> <TD align="right"> 0.51 </TD> <TD> (0.47-0.56) </TD> <TD align="right"> 0.46 </TD> <TD> (0.36-0.58) </TD> </TR>
  <TR> <TD> replica </TD> <TD> head </TD> <TD> all </TD> <TD align="right">  18 </TD> <TD align="right"> 0.51 </TD> <TD> (0.47-0.56) </TD> <TD align="right"> 0.43 </TD> <TD> (0.33-0.57) </TD> </TR>
  <TR> <TD> Elvik </TD> <TD> face </TD> <TD> old </TD> <TD align="right">   8 </TD> <TD align="right"> 0.63 </TD> <TD> (0.56-0.71) </TD> <TD align="right"> 0.56 </TD> <TD> (0.42-0.74) </TD> </TR>
  <TR> <TD> replica </TD> <TD> face </TD> <TD> old </TD> <TD align="right">   8 </TD> <TD align="right"> 0.63 </TD> <TD> (0.56-0.71) </TD> <TD align="right"> 0.56 </TD> <TD> (0.42-0.74) </TD> </TR>
  <TR> <TD> Elvik </TD> <TD> face </TD> <TD> new </TD> <TD align="right">   3 </TD> <TD align="right"> 0.94 </TD> <TD> (0.81-1.1) </TD> <TD align="right"> 1.20 </TD> <TD> (0.72-  2) </TD> </TR>
  <TR> <TD> replica </TD> <TD> face </TD> <TD> new </TD> <TD align="right">   3 </TD> <TD align="right"> 0.94 </TD> <TD> (0.81-1.1) </TD> <TD align="right"> 1.20 </TD> <TD> (0.71-  2) </TD> </TR>
  <TR> <TD> Elvik </TD> <TD> face </TD> <TD> all </TD> <TD align="right">  11 </TD> <TD align="right"> 0.74 </TD> <TD> (0.67-0.81) </TD> <TD align="right"> 0.67 </TD> <TD> (0.52-0.86) </TD> </TR>
  <TR> <TD> replica </TD> <TD> face </TD> <TD> all </TD> <TD align="right">  11 </TD> <TD align="right"> 0.73 </TD> <TD> (0.67-0.81) </TD> <TD align="right"> 0.71 </TD> <TD> (0.55-0.92) </TD> </TR>
  <TR> <TD> Elvik </TD> <TD> neck </TD> <TD> old </TD> <TD align="right">   3 </TD> <TD align="right"> 1.36 </TD> <TD> (  1-1.9) </TD> <TD align="right"> 1.40 </TD> <TD> (0.97-  2) </TD> </TR>
  <TR> <TD> replica </TD> <TD> neck </TD> <TD> old </TD> <TD align="right">   3 </TD> <TD align="right"> 1.36 </TD> <TD> (  1-1.9) </TD> <TD align="right"> 1.40 </TD> <TD> (0.97-  2) </TD> </TR>
  <TR> <TD> Elvik </TD> <TD> neck </TD> <TD> new </TD> <TD align="right">   1 </TD> <TD align="right"> 1.24 </TD> <TD> (0.98-1.6) </TD> <TD align="right"> 1.24 </TD> <TD> (0.98-1.6) </TD> </TR>
  <TR> <TD> replica </TD> <TD> neck </TD> <TD> new </TD> <TD align="right">   1 </TD> <TD align="right"> 1.24 </TD> <TD> (0.98-1.6) </TD> <TD align="right"> 1.24 </TD> <TD> (0.98-1.6) </TD> </TR>
  <TR> <TD> Elvik </TD> <TD> neck </TD> <TD> all </TD> <TD align="right">   4 </TD> <TD align="right"> 1.28 </TD> <TD> (1.1-1.6) </TD> <TD align="right"> 1.29 </TD> <TD> (1.1-1.6) </TD> </TR>
  <TR> <TD> replica </TD> <TD> neck </TD> <TD> all </TD> <TD align="right">   4 </TD> <TD align="right"> 1.28 </TD> <TD> (1.1-1.6) </TD> <TD align="right"> 1.28 </TD> <TD> (1.1-1.6) </TD> </TR>
  <TR> <TD> Elvik </TD> <TD> head/face/neck </TD> <TD> old </TD> <TD align="right">  24 </TD> <TD align="right"> 0.54 </TD> <TD> (0.5-0.59) </TD> <TD align="right"> 0.62 </TD> <TD> (0.52-0.75) </TD> </TR>
  <TR> <TD> replica </TD> <TD> head/face/neck </TD> <TD> old </TD> <TD align="right">  24 </TD> <TD align="right"> 0.54 </TD> <TD> (0.5-0.59) </TD> <TD align="right"> 0.52 </TD> <TD> (0.41-0.66) </TD> </TR>
  <TR> <TD> Elvik </TD> <TD> head/face/neck </TD> <TD> new </TD> <TD align="right">   9 </TD> <TD align="right"> 0.87 </TD> <TD> (0.79-0.95) </TD> <TD align="right"> 1.02 </TD> <TD> (0.84-1.2) </TD> </TR>
  <TR> <TD> replica </TD> <TD> head/face/neck </TD> <TD> new </TD> <TD align="right">   9 </TD> <TD align="right"> 0.87 </TD> <TD> (0.79-0.95) </TD> <TD align="right"> 0.85 </TD> <TD> (0.66-1.1) </TD> </TR>
  <TR> <TD> Elvik </TD> <TD> head/face/neck </TD> <TD> all </TD> <TD align="right">  33 </TD> <TD align="right"> 0.66 </TD> <TD> (0.62-0.7) </TD> <TD align="right"> 0.79 </TD> <TD> (0.69-0.9) </TD> </TR>
  <TR> <TD> replica </TD> <TD> head/face/neck </TD> <TD> all </TD> <TD align="right">  33 </TD> <TD align="right"> 0.66 </TD> <TD> (0.62-0.7) </TD> <TD align="right"> 0.60 </TD> <TD> (0.5-0.73) </TD> </TR>
   </TABLE>


As can be seen from this output, the replication agrees precisely with the fixed-effects summary OR estimates (and confidence intervals) which are given in the Elvik corrigendum. This agreement proves that the underlying data used in this replication are the same as those used by Elvik for the corrigendum.

However, several of the random-effects summary OR estimates are different, some by a considerable margin. This appears to be the case wherever both the old (i.e. Attewell _et al_.) and the new studies are combined (the "all" rows), and for all the combined head, face and neck results. This points to an anomaly in the way in which Elvik has calculated the pooled random-effects summary estimates in his spreadsheet. Close scrutiny of the spreadsheet supplied by Professor Elvik reveals several possible sources of these anomalies, although I cannot be sure because spreadsheets are difficult to debug and reverse-engineer at the best of times, and doubly so when constructed by someone else. Nonetheless, the Elvik results as they appear in the corrigendum do appear to be irreproducible.

Could the R _meta_ package be wrong? This is unlikely because it has been available for many years and has been widely used. Nevertheless, as an additional check, I replicated the meta-analysis in Stata 12.1 using the _metan_ add-in. This produced exactly the same results as the _meta_ package in R.

Elvik bases the conclusions to his paper (both the original and corrected versions) on the publication bias adjusted random-effects summary estimates for both old and new studies combined, and for head, face and neck outcomes combined. Unfortunately, these are the very results which are affected by the calculation anomalies which are apparent in the corrigendum.

How significant are the discrepancies? Elvik states in his conclusion: 
> When the analysis is updated by adding four new studies, the protective effects attributed to to bicycle helmets are further reduced. According to the new studies, no overall effect of bicycle helmets could be found when injuries to head, face or neck are considered as a whole.

Presumably this conclusion was drawn on the basis of the publication-bias-adjusted fixed-effects and random-effects summary ORs for head, face and neck outcomes combined, as given by Elvik in Table 4 of the corrigendum. For the "new" studies, these are: fixed-effects OR=0.89 (95% CI 0.82 - 0.98) and random-effects OR=1.03 (95% CI 0.86 - 1.24).

Let's try to replicate those results:

```r
studies.hfn.new <- studies[which(studies$injury.type %in% c("head", "face", 
    "neck") & studies$meta.analysis == "E"), ]
hfn.new.meta <- metagen(TE = yi, seTE = sei, studlab = study.label, data = studies.hfn.new, 
    method.bias = "rank", label.e = "Injured", label.c = "Not injured", sm = "OR")
hfn.new.tf <- trimfill(hfn.new.meta)
summary(hfn.new.tf)
```

```
## Number of studies combined: k=10 (with 1 added studies)
## 
##                        OR         95%-CI      z  p.value
## Random effects model 0.88 [0.673; 1.151] -0.933   0.3508
## 
## Quantifying heterogeneity:
## tau^2 = 0.1173; H = 2.3 [1.72; 3.07]; I^2 = 81.1% [66.2%; 89.4%]
## 
## Test of heterogeneity:
##      Q d.f.  p.value
##  47.52    9 < 0.0001
## 
## Details on meta-analytical method:
## - Inverse variance method
## - DerSimonian-Laird estimator for tau^2
## - Trim-and-fill method to adjust for funnel plot asymmetry
```

The _trimfill()_ function in _meta_ only adds one hypothetical fill study, whereas Elvik adds two, which is why the adjusted fixed-effects summary OR produced by R is slightly different to the Elvik result (R: 0.87, Elvik: 0.89), but the adjusted **random-effects** summary OR from R is nowhere near that reported by Elvik in the corrigendum (R: 0.88, Elvik: 1.03). Similarly, the "headline" result of the Elvik meta-analysis has been the publication bias-adjusted random-effects summary OR for all studies, both old and new, for head, face and neck injuries combined. In the original (and much quoted) paper, Elvik calculates this as 0.85 (95% CI 0.74 - 0.98), and in the corrigendum, as 0.82 (95% CI 0.72 - 0.93). Here is what we get:

```
## Number of studies combined: k=39 (with 6 added studies)
## 
##                         OR        95%-CI      z  p.value
## Random effects model 0.673 [0.552; 0.82] -3.929 < 0.0001
## 
## Quantifying heterogeneity:
## tau^2 = 0.2448; H = 2.7 [2.37; 3.07]; I^2 = 86.2% [82.1%; 89.4%]
## 
## Test of heterogeneity:
##       Q d.f.  p.value
##  276.25   38 < 0.0001
## 
## Details on meta-analytical method:
## - Inverse variance method
## - DerSimonian-Laird estimator for tau^2
## - Trim-and-fill method to adjust for funnel plot asymmetry
```

Clearly, a summary odds-ratio of 0.67 is materially different to a summary odds-ratio of 0.82, or 0.85.

I wrote to Professor Elvik and his co-editor Dr Karl Kim on 30th December 2012 to alert them to these apparent calculation errors in the corrigendum, once again providing data files and both R and Stata code in support of my findings. It now seems clear that both the original Elvik meta-analysis and the corrigendum ought to be retracted in their entirety, given the pervasive nature of these calculation problems. Publication of a whole-of-paper corrigendum for a whole-of-paper corrigendum would be untenable: Elvik should be required to go back to square one and re-submit a completely new paper for a completely fresh and, it is hoped, more thorough peer-review. To date, I have been notified by an Elsevier representative that the matter is under investigation. Note that there is no hint whatsoever of falsification or any deliberate wrong-doing in any of this - these are all just unfortunate mistakes, albeit ones which might have been avoided or detected earlier had things been done differently.

Can the results in this document be used as replacements for Elvik's results?
-----------------------------------------------------------------------------
From a purely numerical perspective, the replicated results given above are almost certainly correct: it is very difficult to see how the data and R code used in this document could produce an entire set of fixed-effects results and some random-effects results which are identical to Elvik's, but other random-effects results which are different. Either Elvik or the _meta_ package for R must be wrong, and it is very unlikely that it is the R package that is at fault.

However, from an epidemiological perspective, the results in this document strongly suggest that Elvik's results should not be relied upon and should be set aside, but that is all. They should not be used or cited as replacements for Elvik's results, for the following reasons. Firstly, this document is self-published and has not been formally peer-reviewed (although of course it and all the methods and data it uses are completely open to independent scrutiny). Secondly, the analysis presented above only seeks to be an exact replica of the Elvik meta-analysis, intended to illustrate calculation problems. It does not address other issues with the Elvik paper, such as how likely it is that publication bias is actually present in the literature (Elvik just assumes that it is), and whether publication bias adjustment methods can validly be applied to a heterogenous set of studies which assess different injury outcomes (head, face and neck) for which bicycle helmets appear to offer quite different levels of protection (substantial, some, and none at all, respectively). Thirdly, since Elvik undertook his meta-analysis, several new studies of helmet effectiveness have been published, and these deserve to be incorporated into an up-to-date meta-analysis, building, as Elvik did, on the work of Attewell _et al_.
 
Conclusions and Recommendations
-------------------------------
1. Professor Elvik must be congratulated for freely sharing the spreadsheet which contained both the data that he used and the calculations that he performed on that data. Although it would have been possible to replicate the meta-analysis without this, quite a lot more time and expense would have been involved. Of course, there is no reason why the raw data should not routinely be made available as a supplement to **every** published meta-analysis - ideally in machine-readable format to avoid transcription errors! There are no confidentiality concerns in meta-analyses, because the data is harvested from already-published papers, albeit sometimes laboriously.

2. There is a strong case to be made for authors routinely making their programme code (including spreadsheets) available to both peer reviewers and readers, even if the data can't be released for confidentiality or other reasons. Separating data and calculations is often more difficult with a spreadsheet, but it can be done. If data cannot be released (which is not the case for meta-analyses - it always can be made available), then dummy data can be substituted so that at least the formulas and algorithms used to conduct the research can be scrutinised. 

3. It is rarely advisable to undertake complex epidemiological and statistical calculations using a spreadsheet, especially when well-tested software packages which do the same calculations are readily available. Spreadsheets are just too hard to debug and audit.

Postscript
----------

After a great deal of further correspondence during the balance of 2013, mainly with the publisher, due to the requirement for Elvik, being both author and editor, to recuse himself of further involvement, Elsevier decided that even though the corrigendum was also wrong, it did not need to be retracted, and instead could simply be silently corrected online. This they did, and the version of the corrigendum which now appears online and which is in print (finally!) contains the correct results for both fixed effects amd random effects. Remarkably, the conclusions drawn by Elvik in this corrected-corrigendum have not changed at all from those in the original paper, despite the results of the meta-analysis being significantly different. There is no indication that the paper has been subject to any further peer review, otherwise surely the reviewers would have asked for the conclusions to be updated to refelected the changed numerical results. I find this remarkable, or more precisely, remarkably poor practice on the part of a major scientific publisher. The best interpretation that I can apply to these events is that Elsevier acted in this way in order to save face, given that Elvik was both the editor of the journal and the author of the erroneous paper published in it. One would hope that most papers containing such pervasive calculation errors, in which the author gets it wrong twice, once in the original paper, and then again in the corrigendum, would simply be retracted without further ado.

It should also be noted that Elvik and Kim are no longer the editors of _Accident Analysis and Prevention_ - they were replaced late in 2013. It is unknown whether this change of editors was causally related in any way to the events described above -- I suspect that Elsevier would deny any link.

----

References
----------
([Attewell 2000]) Attewell, RG, Glase, K, McFadden, M (2000). Bicycle Helmets and Injury Prevention: A formal review. Canberra, Australia: Australian Transport Safety Bureau. ISBN 0 642 25514 8 

([Attewell 2001]) Attewell, RG; Glase K, McFadden M (May 2001). Bicycle helmet efficacy: a meta-analysis. Accident Analysis & Prevention 33(3): 45–352. doi:10.1016/S0001-4575(00)00048-8. PMID: 11235796

([Duval & Tweedie 2000]) Duval S, Tweedie R. (2000) Trim and fill: A simple funnel-plot-based method of testing and adjusting for publication bias in meta-analysis. Biometrics. 2000 Jun;56(2):455-63. PMID: 10877304 

([Elvik 2011a]) Elvik R (2011). Publication bias and time-trend bias in meta-analysis of bicycle helmet efficacy: A re-analysis of Attewell, Glase and McFadden, 2001, Accident Analysis & Prevention, Volume 43, Issue 3, May 2011, Pages 1245-1251. PMID: 21376924

([Elvik 2011b]) Elvik R. (2011) Effects of Mobile Phone Use on Accident Risk: Problems of Meta-Analysis When Studies Are Few and Bad. Transportation Research Record: Journal of the Transportation Research Board Issue 2236 pp 20-26.

([Elvik 2012a]) Elvik R. Risk of road accident associated with the use of drugs: A systematic review and meta-analysis of evidence from epidemiological studies. Accident Analysis & Prevention, Withdrawn Article in Press, Available online 9 July 2012. PMID: 22785089

([Elvik 2012b]) Elvik R. (2012). The range of replications technique for assessing the external validity of road safety evaluation studies. Accident Analysis & Prevention Volume 45, March 2012, Pages 272–280. PMID: 22269510

([Elvik 2012c]) Elvik R (2012). Corrigendum to: 'Publication bias and time-trend bias in meta-analysis of bicycle helmet efficacy: A re-analysis of Attewell, Glase and McFadden, 2001' [Accid. Anal. Prev. 43 (2011) 1245–1251]. Accident Analysis & Prevention, In Press, Corrected Proof, Available online 23 December 2012.

([Høye & Elvik 2010]) Høye A, Elvik R (2010). Publication Bias in Road Safety Evaluation: How Can It Be Detected and How Common Is It? Transportation Research Record: Journal of the Transportation Research Board Volume 2147 pp 1-8.

----

### Conflicts of interest
None. I am the co-author of two papers on the effects of mandatory bicycle helmet laws in Australia, both published in _Accident Analysis & Prevention_ ([Walter _et al_. 2011], [Walter _et al_. 2013]) and am currently working on an updated meta-analysis of bicycle helmet effectiveness, based on the work described in this article, as an unfunded project in my spare time. I have no relationship with and receive no funding or remuneration from any helmet manufacturer, wholesaler or retailer, nor any government departments or committees with responsibility for cycling or road safety policy.

----

[Attewell 2000]: http://www.infrastructure.gov.au/roads/safety/publications/2000/pdf/Bic_Crash_5.pdf "Attewell, RG, Glase, K, McFadden, M (2000). Bicycle Helmets and Injury Prevention: A formal review. Canberra, Australia: Australian Transport Safety Bureau. ISBN 0 642 25514 8" 

[Attewell 2001]: http://www.sciencedirect.com/science/article/pii/S0001457500000488 "Attewell, RG; Glase K, McFadden M (May 2001). Bicycle helmet efficacy: a meta-analysis. Accident Analysis & Prevention 33(3): 45–352. doi:10.1016/S0001-4575(00)00048-8. PMID: 11235796"

[Duval & Tweedie 2000]: http://www.ncbi.nlm.nih.gov/pubmed/10877304 "Duval S, Tweedie R. (2000) Trim and fill: A simple funnel-plot-based method of testing and adjusting for publication bias in meta-analysis. Biometrics. 2000 Jun;56(2):455-63. PMID: 10877304" 

[Elvik 2011a]: http://dx.doi.org/10.1016/j.aap.2011.01.007 "Elvik R (2011). Publication bias and time-trend bias in meta-analysis of bicycle helmet efficacy: A re-analysis of Attewell, Glase and McFadden, 2001, Accident Analysis & Prevention, Volume 43, Issue 3, May 2011, Pages 1245-1251. PMID: 21376924"

[Elvik 2011b]: http://dx.doi.org/10.3141/2236-03 "Elvik R. (2011) Effects of Mobile Phone Use on Accident Risk: Problems of Meta-Analysis When Studies Are Few and Bad. Transportation Research Record: Journal of the Transportation Research Board Issue 2236 pp 20-26."

[Elvik 2012a]: http://dx.doi.org/10.1016/j.aap.2012.06.017 "Elvik R. Risk of road accident associated with the use of drugs: A systematic review and meta-analysis of evidence from epidemiological studies. Accident Analysis & Prevention, Withdrawn Article in Press, Available online 9 July 2012. PMID: 22785089"

[Elvik 2012b]: http://dx.doi.org/10.1016/j.aap.2011.07.016 "Elvik R. (2012). The range of replications technique for assessing the external validity of road safety evaluation studies. Accident Analysis & Prevention Volume 45, March 2012, Pages 272–280. PMID: 22269510"

[Elvik 2012c]: http://dx.doi.org/10.1016/j.aap.2012.12.003 "Elvik R (2012). Corrigendum to: 'Publication bias and time-trend bias in meta-analysis of bicycle helmet efficacy: A re-analysis of Attewell, Glase and McFadden, 2001' [Accid. Anal. Prev. 43 (2011) 1245–1251]. Accident Analysis & Prevention, In Press, Corrected Proof, Available online 23 December 2012."

[Høye & Elvik 2010]: http://dx.doi.org/10.3141/2147-01 "Høye A, Elvik R (2010). Publication Bias in Road Safety Evaluation: How Can It Be Detected and How Common Is It? Transportation Research Record: Journal of the Transportation Research Board Volume 2147 pp 1-8."

[Walter _et al_. 2011]: http://handle.unsw.edu.au/1959.4/50858 "Walter SR, Olivier J, Churches T, Grzebieta R. (November 2011). "The impact of compulsory cycle helmet legislation on cyclist head injuries in New South Wales, Australia.". Accident Analysis & Prevention 43 (6): 2064–2071. doi:10.1016/j.aap.2011.05.029. PMID: 21819836"

[Walter _et al_. 2013]: http://handle.unsw.edu.au/1959.4/52350 "Walter SR, Olivier J, Churches T, Grzebieta R. (March 2013). "The impact of compulsory helmet legislation on cyclist head injuries in New South Wales, Australia: A response". Accident Analysis & Prevention 52: 204–209. doi:10.1016/j.aap.2012.11.028. PMID: 23339779"
