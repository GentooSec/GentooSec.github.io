---
title:  "¡Migration!"
date:   2018-12-21
published: true
---

This is a small post to analyze migrations using a package called [**migest**](https://cran.r-project.org/web/packages/migest/index.html), this is simply to provide methods for indirect estimation of bilateral migration. It is no secret that Venezuelan migration is not a problem in that country. The good thing about this package is that it has an example, which we will show below:
The first thing is to start loading our libraries and then we generate the demo

~~~R
library("migest")
demo(cfplot_reg, package = "migest", ask = FALSE)
~~~
Generating the following circular plot 

![](/images/migra_demo.png)

Now to work with real data, for them we will use one of the many sources that exist, for example [**IRIS**](https://www.irs.gov/statistics/soi-tax-stats-migration-data-2015-2016)

It is a pretty complete and nice example, although we can do it in a more personalized way. Playing with all the options that it has. In our case alone we will use a few data of sample and also we could use alone Latin America or some specific continent that we wanted, but in order that it is better visualized we will use the complete dataset.

~~~R
uno <- read.csv(system.file("vidwp", "reg_flow.csv", package = "migest"), stringsAsFactors=FALSE)
dos <- read.csv(system.file("vidwp", "reg_plot.csv", package = "migest"), stringsAsFactors=FALSE)

chordDiagram(x = uno)
~~~

It is important to mention that our cvs data are:

~~~R
print(uno)
                       orig_reg                      dest_reg     flow
1                         Africa                        Africa 3.498892
2                         Africa                  Eastern Asia 0.007214
3                         Africa Eastern Europe & Central Asia 0.036820
4                         Africa                        Europe 1.744666
5                         Africa     Latin America & Caribbean 0.022516
6                         Africa              Northern America 0.825409
7                         Africa                       Oceania 0.107072
8                         Africa                 Southern Asia 0.000869
9                         Africa                  Western Asia 0.675984
10                  Eastern Asia                        Africa 0.021043
11                  Eastern Asia                  Eastern Asia 2.178887
12                  Eastern Asia Eastern Europe & Central Asia 0.085849
13                  Eastern Asia                        Europe 0.565937
14                  Eastern Asia     Latin America & Caribbean 0.040990
15                  Eastern Asia              Northern America 1.593311
16                  Eastern Asia                       Oceania 0.359676
17                  Eastern Asia                 Southern Asia 0.002097
18                  Eastern Asia                  Western Asia 0.380948
19 Eastern Europe & Central Asia                        Africa 0.001760
20 Eastern Europe & Central Asia                  Eastern Asia 0.025689
21 Eastern Europe & Central Asia Eastern Europe & Central Asia 1.354018
22 Eastern Europe & Central Asia                        Europe 0.566555
23 Eastern Europe & Central Asia     Latin America & Caribbean 0.001438
24 Eastern Europe & Central Asia              Northern America 0.043438
25 Eastern Europe & Central Asia                       Oceania 0.002543
26 Eastern Europe & Central Asia                 Southern Asia 0.000000
27 Eastern Europe & Central Asia                  Western Asia 0.088158
28                        Europe                        Africa 0.175242
29                        Europe                  Eastern Asia 0.010825
30                        Europe Eastern Europe & Central Asia 0.601772
31                        Europe                        Europe 2.006166
32                        Europe     Latin America & Caribbean 0.168391
33                        Europe              Northern America 0.449838
34                        Europe                       Oceania 0.222712
35                        Europe                 Southern Asia 0.000014
36                        Europe                  Western Asia 0.223626
37     Latin America & Caribbean                        Africa 0.004648
38     Latin America & Caribbean                  Eastern Asia 0.014653
39     Latin America & Caribbean Eastern Europe & Central Asia 0.009782
40     Latin America & Caribbean                        Europe 0.290048
41     Latin America & Caribbean     Latin America & Caribbean 0.682464
42     Latin America & Caribbean              Northern America 2.195385
43     Latin America & Caribbean                       Oceania 0.022709
44     Latin America & Caribbean                 Southern Asia 0.000000
45     Latin America & Caribbean                  Western Asia 0.010966
46              Northern America                        Africa 0.011244
47              Northern America                  Eastern Asia 0.044196
48              Northern America Eastern Europe & Central Asia 0.172959
49              Northern America                        Europe 0.213784
50              Northern America     Latin America & Caribbean 0.207948
51              Northern America              Northern America 0.112105
52              Northern America                       Oceania 0.037692
53              Northern America                 Southern Asia 0.000000
54              Northern America                  Western Asia 0.026320
55                       Oceania                        Africa 0.006264
56                       Oceania                  Eastern Asia 0.006773
57                       Oceania Eastern Europe & Central Asia 0.015882
58                       Oceania                        Europe 0.079224
59                       Oceania     Latin America & Caribbean 0.004123
60                       Oceania              Northern America 0.045753
61                       Oceania                       Oceania 0.184822
62                       Oceania                 Southern Asia 0.000000
63                       Oceania                  Western Asia 0.011272
64                 Southern Asia                        Africa 0.051368
65                 Southern Asia                  Eastern Asia 0.505476
66                 Southern Asia Eastern Europe & Central Asia 0.042952
67                 Southern Asia                        Europe 1.168379
68                 Southern Asia     Latin America & Caribbean 0.009744
69                 Southern Asia              Northern America 1.420783
70                 Southern Asia                       Oceania 0.316133
71                 Southern Asia                 Southern Asia 1.306389
72                 Southern Asia                  Western Asia 3.106273
73                  Western Asia                        Africa 0.244112
74                  Western Asia                  Eastern Asia 0.007958
75                  Western Asia Eastern Europe & Central Asia 0.395673
76                  Western Asia                        Europe 0.431518
77                  Western Asia     Latin America & Caribbean 0.006412
78                  Western Asia              Northern America 0.323827
79                  Western Asia                       Oceania 0.065140
80                  Western Asia                 Southern Asia 0.036058
81                  Western Asia                  Western Asia 4.519158
~~~

The result! 

![](/images/america.png)

~~~R
HACKED!
~~~
