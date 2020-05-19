---
layout: post
title:  "Exploring Chicago: Where Should You Live Pt1"
date:   2020-05-17
categories: R EDA
---

A friend was telling me he was thinking about becoming a first-time homeowner in Chicago. We bantered back and forth about neighborhoods that were top contenders and the pros and cons of each. If you don’t live in Chicago, know that where you live in the city can yield totally different experiences, and those experiences can even vary from block to block. That prompted me to want to bring some data into the equation to fuel this conversation. I will do a three part analysis. In this post, I'll analyze trends in demographic census data, and what they mean for the city. The next post will bring in city data such as business licenses and crime. Finally I'll bring all these elements together in a tool that could assist an individual in identifying ideal areas for them.  

For this analysis I pulled census data at the census block group level for Cook County, Chicago. This data included variables on income, race, education, employment, and population, but I will only be focusing on income, race, and population in this post. 

![neighborhood map](https://www.dropbox.com/s/63bd55gphfh5wnq/Neighborhood_Map.png?raw=1)  


**Money Money Money**   

Do people who have similar income levels, live in the same places? My guess is yes, and I bet that greatly impacts the character of those spaces. I looked at median household income to gain some insight.  

Chicago block groups have median household incomes ranging from $6800 to over $210,000 and the median across all block groups is about $48K. That’s a huge range, and the median indicates that the majority of block groups are closer to the lower end than the higher. 
Looking at the histogram below, you can see how skewed the distribution of household income is across the different block groups.  


![income_histogram](https://www.dropbox.com/s/jqz84krq1vdl2wa/income_histogram.png?raw=1)   

Spatially, we can see that higher incomes are concentrated in certain parts of the city. The north side neighborhoods are mostly among the highest incomes, while the west and south sides are amongst the lowest. However, looking at the Chicago map colored at the block group level, we see that there are sprinkles of low income blocks on the north side and sprinkles of higher income blocks in the south side neighborhoods.  

![comm_inc_dec_map](https://www.dropbox.com/s/tdnsvwpai2qpcyh/cmnty_income_deciles_map.png?raw=1) ![bg inc dec map](https://www.dropbox.com/s/zmczkqb6bt7j6cb/bg_income_deciles_map.png?raw=1)    

To drive home the point about household income diversity within neighborhoods, below you can see a boxplot of median household income by community area (CA). For each CA, the boxplot represents the distribution of incomes at the block group level. The line in the middle of the plot represents the median (50th percentile) of block group median household incomes for that CA, and the edges of the box represent the 25th and 75th income percentiles respectively. The communities are sorted from lowest average median household income to highest.   

![cmnty-income-boxplot](https://www.dropbox.com/s/vp97kknohdsl1ve/cmnty-income-boxplot.png?raw=1)   

One interesting observation is that lower income CA’s tend to have a smaller range of block group incomes, ie less income diversity, whereas the top income CA’s have a broader range of incomes. Take note of Lincoln Park, Near West Side, and Near South Side. These CA’s have block groups whose median household income range from $25K to upwards of $150K. For neighborhoods like Near West Side, this may have to do with the fact that it’s a larger neighborhood, or perhaps that that area, which used to be low-income as exemplified by previously housing the Cabrini-Green projects has faced a lot of gentrification, and so may be in a transitional phase. However, there may be something else going on here, since neighborhoods like Lincoln Park have long been established as being amongst the “nicer” neighborhoods.   

**Race**  

Chicago has a reputation for being amongst the most segregated cities in the US. When I looked at the data, this reputation was confirmed.  I took the population counts by race for each block group and created a race population percent metric for white, black, and Asian groups. In the map below, we can see the percentage range of population by race for the three groups at the block group level. The white population percent map shows us lighter colored block groups on the north side, indicating that the north side neighborhoods have a higher percent of white population and we see nearly no white population (less than 10%) for many of the south and west side block groups, which are colored dark.  

![race-percents-bg](https://www.dropbox.com/s/njxn14dy9ipgebo/race_percents_bg.png?raw=1)  

The black population percent map is almost an inverse of the white one, where many of the south and west side block groups have 80%+ black populations. The Asian population percent map shows us that most block groups don’t have a concentration of Asian inhabitants. But there are some areas on the near west side that are mostly Asian (hi Chinatown!) and some small pockets on the north side that are about 30-60% Asian.  

One interesting observation from these maps is that it seems that the white population map shows more areas where the white population is more mid-range (40-70%) particularly in some of the southwest areas, whereas the black population map shows that for the most part, block groups are either overwhelmingly black, or barely black. This may say something about segregation policies in the city, which have historically shaped where black people live. Also, it’s worth noting that these map patterns for black and white are roughly on par with the map patterns for high and low income block groups.  

We can see the stark distribution spectrum for the black population in the histogram below as compared to the white population. The white population percentage median is close to 50% telling us that about half of the block groups have a population percentage above 50% and half below. The black population percentage median is closer to 10%, indicating that half the block groups have a black population that is less than 10%.

![race_histogram](https://www.dropbox.com/s/qdum5dxnw9nvo6n/race_histogram.png?raw=1)     

Note, I know this race analysis is very much focused on black and white, but I wanted to outline the stark contrasts.

**Population**  

The last variable that I wanted to look at was population density. Some neighborhoods are full of high rises, and some are basically all houses or small apartment buildings. I wanted to know if the density of people living in a certain square area could tell us anything about anything. Below you can see a map of the block groups grouped into deciles by their population density.  

![popDensityMap](https://www.dropbox.com/s/me1ayhl01e97o2a/popDensity_map.png?raw=1)  

I was a little surprised to see that many of the north side blocks had the higher population densities. If I think about it though, this makes sense considering that much of the north side is apartment living, very developed, and congested, whereas there are a lot more single family homes in other parts of the city. It was just surprising based on what we saw with income trends, since there’s usually an assumption that lower income areas are packed with people living in very close quarters.  


**Bringing it all Together**  

From looking at the three features, median household income, race, and population density, we can see some clear spatial trends in the city. Racial and income segregation seem to be quite real, and population density may say something about income levels, although not in the way that most people would think.  

Below you can see a correlation plot which ties these relationships together. The scatter plot of white population percent vs income shows a clear upwards relationship with a relatively strong correlation of .62, whereas the plot of black population percent vs. income shows a clear negative relationship. The inverse relationship between black and white populations is insanely strong with a correlation of -.90 (telling us that black and white people don't really live together much). And we see a slight positive relationship between population density and white population percentage and a slight negative relationship between population density and black population percentage.  

![corrplot](https://www.dropbox.com/s/wxzelzv5floqo5n/corrplot.png?raw=1)    

So what does all of this mean? I think it means that if you’re a person looking for a diverse neighborhood, there may not be a ton of options. Racially, the city is very stratified. But what’s more, neighborhoods that are not majority white tend to have less income diversity as well. This may indicate a lack of difference in the type of jobs that people in an area work as well (although this is not supported by data...just a hypothesis). Also, how close you want to live with other people could influence in what part of the city you live.  

In my next post, I will bring in city data to get a better feel for what's happening in the different block group areas. If you’d like to see more detail on this analysis, please check out my [github repo][github-chi1]. There’s a lot of data cleaning that took place for this analysis.  



Sources:   
[https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Community-Areas-current-/cauq-8yn6][city of chicago]    
[https://www.census.gov/cgi-bin/geo/shapefiles/index.php][census]  
2017 American Community Survey Data:  [https://www.nhgis.org][nhgis]  



[github-chi1]: https://github.com/ljshores/Exploring_Chicago
[city of chicago]: https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Community-Areas-current-/cauq-8yn6
[census]: https://www.census.gov/cgi-bin/geo/shapefiles/index.php
[nhgis]: https://www.nhgis.org
