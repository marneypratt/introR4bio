R Code for Grouped Graphs Swirl Lesson
================
Marney Pratt
8/22/2020

# Load Packages and Import Data

``` r
# load packages
library(readr) ##for importing data
library(ggplot2)  ##for graphing
library(dplyr) ## for filtering, summarising, and other data wrangling
library(ggbeeswarm) #for making symmetrical jittering (beeswarm) of points
library(curl) #used for loading data from websites


# import hemlock data file
hemlock <- read_csv("https://docs.google.com/spreadsheets/d/e/2PACX-1vT-Uo5Gs2dcR6f6_PFrZwkaSrojsBCFt1qvVNU0PXn4RHVe3_GDzNL3BCxkkp6eIhjkfKw3S6YcX6wz/pub?output=csv", 
                    col_types = cols(SamplingDate = col_date(format = "%m/%d/%Y"), 
                                     Location = col_factor()))
```

# Bar Graph of Means and Standard Errors

``` r
# calculate descriptive stats and SE for EHS density
EHS.sum <- hemlock %>%
  group_by(Location) %>%
  summarise(mean = mean(EHS), 
            sd = sd(EHS), 
            n = n()) %>%
  mutate(sem = sd/(sqrt(n)))


# Bar plot with mean and SE
g.bar <- ggplot(EHS.sum, aes(x=Location,y=mean, fill))+
  geom_bar(stat="identity",  width = 0.5, show.legend=FALSE, fill = "steelblue")+
  geom_errorbar(aes(ymin=mean-sem, ymax=mean+sem), width=0.1, size=1) +
  ylab("EHS Density (insects/cm)") +
  xlab("Location") +
  coord_cartesian(xlim = c(0.5,4.5), expand=FALSE) +
  theme_classic(base_size=16) 
print(g.bar)
```

![](Graphing_Grouped_Continuous_Data-code_files/figure-gfm/bar%20with%20SE-1.png)<!-- -->

``` r
# save the graph
ggsave(path="figures", filename="bar.jpg", height = 7, width = 8, units = "in", dpi = 500)
```

# Histograms

A histogram is only useful when there are enough data points. A good
rule of thumb is that a histogram is useful when your sample size in
each group is 20-30 or more. If your N \< 20 for each group, then it may
not be useful to visualize with a histogram.

``` r
 # To make a histogram of just one location, first you have to filter for a location (in this case FLH)
FLH.data <- hemlock %>% filter(Location == "FLH")

# Histogram of the EHS density at the FLH location
# change the binwidth as needed
FLH.hist <- ggplot(data = FLH.data, aes(x = EHS))+ 
  geom_histogram(binwidth = 0.4, color = "white", fill = "steelblue", show.legend = FALSE) +
  xlab("EHS Density (insects/cm)") +
  ylab("Count") +
  coord_cartesian(expand=TRUE) +
  theme_classic(base_size=14) 
print(FLH.hist)
```

![](Graphing_Grouped_Continuous_Data-code_files/figure-gfm/histogram-1.png)<!-- -->

``` r
# Histogram of the HWA density for all 4 locations
g.hist <- ggplot(data = hemlock, aes(x = EHS, fill=Location))+ 
  geom_histogram(binwidth = 0.4, color = "white", show.legend = FALSE) +
  facet_grid(Location ~ .) +
  xlab("EHS Density (insects/cm)") +
  ylab("Count") +
  coord_cartesian(expand=TRUE) +
  theme_classic(base_size=14) 
print(g.hist)
```

![](Graphing_Grouped_Continuous_Data-code_files/figure-gfm/histogram-2.png)<!-- -->

``` r
# save the graph
ggsave(path="figures", filename="histogram.jpg", height = 7, width = 8, units = "in", dpi = 500)
```

# Box Plots

Type ?geom\_boxplot in the console or search for geom\_boxplot in the
help window to pull up the help file. Scroll down to “Summary
statistics” to make sure you understand what the box plot is showing
and describe ALL the symbols accurately in your figure legend.

Remember, box plots are not useful for very small sample sizes (\< 20 or
so). You need an absolute minimum of 5 points, but it is better to have
more points for a box plot. If your N \< 10 for each group, then it is
probably not useful to visualize with a box plot.

## Plain Box Plots with Means

This code will give a box plot with the mean indicated. Points indicate
outliers

``` r
# Box plot of the EHS density at all 4 locations, X = mean
# Erase the stat_summary function if you want to remove the mean
EHS.box <-ggplot(data = hemlock, aes(x= Location, y = EHS, color=Location))+ 
  stat_boxplot(geom ='errorbar', width = 0.1,  na.rm = TRUE, lwd=0.75, show.legend = FALSE) +
  geom_boxplot(width = 0.5, na.rm = TRUE,lwd=0.75, show.legend = FALSE) +
  stat_summary(fun=mean, geom="point",  shape=4, size=2,  
               na.rm = TRUE, show.legend = FALSE, colour = "black", stroke = 2) +
  ylab("EHS Density (insects/cm)") +
  xlab("Location") +
  coord_cartesian(ylim=c(0,11.5),expand=TRUE) +
  theme_classic(base_size=20) 
print(EHS.box)
```

![](Graphing_Grouped_Continuous_Data-code_files/figure-gfm/plain%20box-1.png)<!-- -->

``` r
# save the graph
ggsave(path="figures", filename="box.jpg", height = 7, width = 8, units = "in", dpi = 500)
```

## Box Plots with Random Jittered Points

This code will give a box plot with the mean indicated and all points
are included and randomly jittered to avoid overlapping

``` r
# Box plot of the EHS density at all 4 locations, X = mean, all points randomly jittered
# Erase the stat_summary function if you want to remove the mean
EHS.box2 <-ggplot(data = hemlock, aes(x= Location, y = EHS))+ 
  geom_point(aes(x= Location, y = EHS, fill = Location), shape=21, size=1, alpha = 0.5,
             position=position_jitterdodge(jitter.width=0.8), show.legend=FALSE) +
  stat_boxplot(geom ='errorbar', width = 0.1,  na.rm = TRUE, lwd=0.75) +
  geom_boxplot(width = 0.5, na.rm = TRUE, outlier.shape= NA, alpha = 0.1, lwd=0.75) +
  stat_summary(fun=mean, geom="point",  shape=4, size=2,  
               na.rm = TRUE, show.legend = FALSE, colour = "black", stroke = 2) +
  ylab("EHS Density (insects/cm)") +
  xlab("Location") +
  coord_cartesian(expand=TRUE) +
  theme_classic(base_size=20) 
print(EHS.box2)
```

![](Graphing_Grouped_Continuous_Data-code_files/figure-gfm/box%20plus%20random%20jittered%20points-1.png)<!-- -->

``` r
# save the graph
ggsave(path="figures", filename="box_random.jpg", height = 7, width = 8, units = "in", dpi = 500)
```

## Box Plots with symmetric jittered points - beeswarm

This code will give a box plot with the mean indicated and all points
are included and symmetrically jittered with beeswarm

``` r
# Box plot of the EHS density at all 4 locations, X = mean, 
# all points symmetrically jittered with beeswarm
# Erase the stat_summary function if you want to remove the mean
EHS.box3 <-ggplot(data = hemlock, aes(x= Location, y = EHS))+ 
  geom_beeswarm(aes(x= Location, y = EHS, fill=Location), shape=21, size=1, 
                   alpha=0.5, priority = "random", show.legend=FALSE) +
  stat_boxplot(geom ='errorbar', width = 0.1,  na.rm = TRUE, lwd=0.75) +
  geom_boxplot(width = 0.5, na.rm = TRUE, outlier.shape= NA, alpha = 0.1, lwd=0.75) +
  stat_summary(fun=mean, geom="point",  shape=4, size=2,  
               na.rm = TRUE, show.legend = FALSE, colour = "black", stroke = 2) +
  ylab("EHS Density (insects/cm)") +
  xlab("Location") +
  coord_cartesian(expand=TRUE) +
  theme_classic(base_size=20) 
print(EHS.box3)
```

![](Graphing_Grouped_Continuous_Data-code_files/figure-gfm/box%20plus%20beeswarm%20points-1.png)<!-- -->

``` r
# save the graph
ggsave(path="figures", filename="box_beeswarm.jpg", height = 7, width = 8, units = "in", dpi = 500)
```

## Box Plots with symmetric jittered points - quasirandom

This code will give a box plot with the mean indicated and all points
are included and symmetrically jittered with quasirandom

``` r
# Box plot of the EHS density at all 4 locations, X = mean, 
# all points symmetrically jittered with quasirandom
# Erase the stat_summary function if you want to remove the mean
EHS.box4 <-ggplot(data = hemlock, aes(x= Location, y = EHS))+ 
  geom_quasirandom(aes(x= Location, y = EHS, fill=Location), shape=21, size=1, 
                   alpha=0.5, width=0.3, show.legend=FALSE) +
  stat_boxplot(geom ='errorbar', width = 0.1,  na.rm = TRUE, lwd=0.75) +
  geom_boxplot(width = 0.5, na.rm = TRUE, outlier.shape= NA, alpha = 0.1, lwd=0.75) +
  stat_summary(fun=mean, geom="point",  shape=4, size=2,  
               na.rm = TRUE, show.legend = FALSE, colour = "black", stroke = 2) +
  ylab("EHS Density (insects/cm)") +
  xlab("Location") +
  coord_cartesian(expand=TRUE) +
  theme_classic(base_size=20) 
print(EHS.box4)
```

![](Graphing_Grouped_Continuous_Data-code_files/figure-gfm/box%20plus%20quasirandom%20points-1.png)<!-- -->

``` r
# save the graph
ggsave(path="figures", filename="box_quasi.jpg", height = 7, width = 8, units = "in", dpi = 500)
```

# Violin Plots

If the sample size is very large, it can be helpful to use a violin plot
that shows the distribution (kind of like a probability density curve
mirrored on its side)

``` r
# calculate the sample size for each group first 
sample_size = hemlock %>% group_by(Location) %>% summarize (num=n())

# violin plot with box plots and sample sizes
EHS.violin <- hemlock %>% 
  left_join(sample_size) %>% 
  mutate(myaxis = paste0(Location, "\n", "n=", num)) %>% 
  ggplot(aes(x=myaxis, y=EHS, fill=Location)) +
    geom_violin(width=1.4) +
    geom_boxplot(width=0.08, color="black") +
    ylab("EHS Density (insects/cm)") +
    xlab("Location") +
    theme_classic(base_size=18) +
    theme(legend.position="none")
print(EHS.violin)
```

![](Graphing_Grouped_Continuous_Data-code_files/figure-gfm/violin-1.png)<!-- -->

``` r
# save the graph
ggsave(path="figures", filename="violin.jpg", height = 7, width = 8, units = "in", dpi = 500)
```

# Dot Plots

An increasingly popular way of visualizing data when the sample size is
small enough is to show all the points and a measure of central
tendency. Below are three options for how to add points (1) random
jitter, (2) beeswarm, (3) quasirandom.

These examples all use the mean, to make graphs with the median, just
replace the word mean with median everywhere in the graph.

## Dot Plots with Random Jitter

``` r
# Filter for one semester (Winter 2019)
hemlock$SamplingDate <- as.Date(hemlock$SamplingDate, "%m/%d/%Y")
small <- hemlock %>% filter (SamplingDate > as.Date("2018-11-20"))

# Dot plot with mean
dot.mean <-  ggplot(data = small, aes(x= Location, y = EHS))+ 
  geom_point(aes(x= Location, y = EHS, fill = Location), shape=21, size=3, alpha=0.75,
             position=position_jitterdodge(jitter.width=0.8), show.legend=FALSE) +
  stat_summary(fun = mean, fun.min = mean, fun.max = mean, geom = "crossbar", 
               width = 0.5, size = 0.75, na.rm = TRUE, show.legend = FALSE, colour = "black") +
  ylab("EHS Density (insects/cm)") +
  xlab("Location") +
  coord_cartesian(expand=TRUE) +
  theme_classic(base_size=20) +
  theme(legend.position="none")
print(dot.mean)
```

![](Graphing_Grouped_Continuous_Data-code_files/figure-gfm/dot%20random-1.png)<!-- -->

``` r
# save the graph
ggsave(path="figures", filename="dot.jpg", height = 7, width = 8, units = "in", dpi = 500)
```

## Dot Plots with Symmetric Beeswarm Jitter

``` r
# Filter for one semester (Winter 2019)
hemlock$SamplingDate <- as.Date(hemlock$SamplingDate, "%m/%d/%Y")
small <- hemlock %>% filter (SamplingDate > as.Date("2018-11-20"))

# Dot plot with mean
dot.mean <-  ggplot(data = small, aes(x= Location, y = EHS))+ 
  geom_beeswarm(aes(x= Location, y = EHS, fill=Location), shape=21, size=3, 
                   alpha=0.75, cex=2.25 , priority = "ascending", show.legend=FALSE) +
  stat_summary(fun = mean, fun.min = mean, fun.max = mean, geom = "crossbar", 
               width = 0.5, size = 0.75, na.rm = TRUE, 
               show.legend = FALSE, colour = "black") +
  ylab("EHS Density (insects/cm)") +
  xlab("Location") +
  coord_cartesian(expand=TRUE) +
  theme_classic(base_size=20) +
  theme(legend.position="none")
print(dot.mean)
```

![](Graphing_Grouped_Continuous_Data-code_files/figure-gfm/dot%20beeswarm-1.png)<!-- -->

``` r
# save the graph
ggsave(path="figures", filename="dot_beeswarm.jpg", height = 7, width = 8, units = "in", dpi = 500)
```

## Dot Plots with Symmetric Quasirandom Jitter

``` r
# Filter for one semester (Winter 2019)
hemlock$SamplingDate <- as.Date(hemlock$SamplingDate, "%m/%d/%Y")
small <- hemlock %>% filter (SamplingDate > as.Date("2018-11-20"))

# Dot plot with mean
dot.mean <-  ggplot(data = small, aes(x= Location, y = EHS))+ 
  geom_quasirandom(aes(x= Location, y = EHS, fill=Location), shape=21, size=3, 
                   alpha=0.75, width=0.2, show.legend=FALSE) +
  stat_summary(fun = mean, fun.min = mean, fun.max = mean, geom = "crossbar", 
               width = 0.5, size = 0.75, na.rm = TRUE, 
               show.legend = FALSE, colour = "black") +
  ylab("EHS Density (insects/cm)") +
  xlab("Location") +
  coord_cartesian(expand=TRUE) +
  theme_classic(base_size=20) +
  theme(legend.position="none")
print(dot.mean)
```

![](Graphing_Grouped_Continuous_Data-code_files/figure-gfm/dot%20quasirandom-1.png)<!-- -->

``` r
# save the graph
ggsave(path="figures", filename="dot_quasi.jpg", height = 7, width = 8, units = "in", dpi = 500)
```
