meta-analyses
=============

Data and program code for meta-analyses of population health and health services research questions, as a contribution to reproducible research in these fields.

All files from https://github.com/timchurches/meta-analyses are copyright Tim Churches, but are available at no cost for use by others under the terms of the Creative Commons Attribution-ShareAlike 3.0 Australia license (see http://creativecommons.org/licenses/by-sa/3.0/au/ ).

meta-analyses fork
==================

All files added in this fork are available under the MIT License as shown in their headers.

This version explores whether it is onerous to serialize tabular data as json which gets
converted back to csv files which is what the author's code expects.

[Data Protocols](http://dataprotocols.org/tabular-data-package/) currently recommends serializing
tabular data as csv. I am biased towards using json in APIs and then only falling back on other
formats if there is a reason to. I'm not sure if I feel csv is justified, and this code is my way
of thinking out loud.

some questions

Perhaps we will have code that can take multiple representations, and inspect headers
to act accordingly. How much of that idea is YAGNI? It's been helpful in other situations.

Is it a friction to have javascript that builds a representation in csv versus json? Are we
wanting to be friendly towards clients who want users to interact with their data in a webpage
versus friendly towards clients who make UIs that have users upload csv data?
