---
layout: post
title:  "Exploring Chicago: Where Would You Live - Pt2"
date:   2020-05-26
categories: R EDA
---

In this post we’re going to continue to explore different areas of Chicago with the intention of bringing in data to support pros and cons of living in different areas of the city. I’ll be bringing in data on crime, business licenses, and CTA L access and looking at how these variables relate to the data we explored in the previous post (household income, race, and population).  

![neighborhood map](https://www.dropbox.com/s/63bd55gphfh5wnq/Neighborhood_Map.png?raw=1)  


**Chiraq…? Quit It.**  

There’s no use dodging it…Chicago has a huge reputation for crime. While the city does have some issues, I think that reputation is a bit unfair (maybe I’ll do a post about the data around this some other time). Furthermore, I ABSOLUTELY HATE the title “Chiraq”, which was coined by the media and popular culture because of the amount of reported murders. I’ve heard so many people say they wouldn’t visit Chicago because it’s too unsafe, so let’s explore that. This analysis can’t tell you if Chicago has an abnormally high amount of crime, because I’m only looking at crime counts over the past year, with nothing to compare it with. But I can tell you how crime plays out across the city.  

![perc of all crime by comm map](https://www.dropbox.com/s/z9bm2xmzszkbv17/all_crime_comm_map.png?raw=1)  

The map above shows the percent incidence of all crimes for each community area. Right away you can see that some areas such as Austin, the Near North Side, and the Loop stand out as accounting for a higher percentage of the city’s crimes than some of the other areas. This is interesting because from our prior analysis, we know that these areas are very different. Austin is majority black and has lower incomes whereas the Near North Side and Loop is largely white and has some of the highest median incomes in the city.  

If we look closer into the types of crimes, we see that different crimes are more prevalent in different parts of the city. Below, the map in green shows the incidences of theft, the purple map shows assaults, and the red map shows homicides. There are more thefts in the Loop and Near North Side than any other part of the city. Thefts in these two places make sense, as they are more affluent and more likely to attract tourists, which are ripe for pick-pockets and petty thefts. On the flip side there are more murders and assaults in Austin than other parts of the city. Unfortunately, the homicide map shows patterns akin to the map that highlighted areas of high black population percentages, i.e. more murders are happening in majority black areas than other parts of the city. Just for reference, thefts make up about 24% of the crimes in this data, assaults make up 8% and homicides make up .2% of crimes.  

![theft, homicide, and crime maps in a row](https://www.dropbox.com/s/v8occpla58kiaei/3crime_maps.png?raw=1)

Homicides in any area is a problem that needs to be addressed. However, the data shows that outsider attitudes about Chicago being too dangerous may be overblown. Most out-of-towners go to the Loop, South Loop, Near North Side, Lakeview, and maybe Hyde Park. These areas have had little to no homicides in the past year.  


**The Happening Spots**

I wanted to take a look at how certain business establishments are distributed across the city. When thinking about where to live, access to grocery stores, restaurants, and other forms of entertainment, may be an important factor. So I took a look at registered business licenses in Chicago. Below, you can see the number of business licenses for six groups that I targeted by community area.  

![biz license barplot](https://www.dropbox.com/s/k0lkxwyl3uikxjy/biz_license_barplot.png?raw=1)

The usual suspects like the Loop, the Near North Side, and Lakeview appear to dominate in terms of number of these businesses, especially when it comes to entertainment establishments. Entertainment licenses include "Public Place of Amusement", "Late Hour", "Tavern", "Music and Dance", "Wrigley Field", and, "Navy Pier Kiosk License". The retail food licenses can include anything from a restaurant to a grocery store to a corner store. The maps below give us a better idea of how the businesses are distributed across the city spatially.  

![retail and entertainment map](https://www.dropbox.com/s/uqghlylz7nqv8s8/2_license_map.png?raw=1)  

Being on the lower end of the spectrum for licenses such as retail food doesn’t necessarily imply anything negative or positive about the neighborhood. Forest Glen, which we established had the highest average median household income is on the low end of the spectrum, but that’s just because it is very residential and mostly single family homes. Austin is in the middle of the spectrum for licenses, but is low income. One thing to think about though is if those areas that are on the low end of the spectrum have access to grocery stores. People living in more affluent Forest Glen most likely own cars, whereas some other areas that have lower incomes and not many retail food businesses may find it hard to access good food.  


**Getting Around**  

Living in Chicago, I never owned a car. I relied solely on the CTA L and bus system to get where I needed to go. The L was particularly important because it’s much faster and more reliable than the bus system. So I always made it a point to live within a 15 minute walk to a train station. That being said, I wanted to get a better idea of how the different neighborhoods are served in regards to access to an L station.  

It’s to be expected that the Loop will have heavier L coverage, because that is where most of the train lines converge. But if we take a look at the map below, it seems that the south side of the city has less train station accessibility than the north and west sides.  

![map community L count](https://www.dropbox.com/s/g4zn36hxoai3oub/comm_ctaL_map.png?raw=1)  

The next map shows train station distribution at the block group level and gives a rough idea of the train lines that run through the city.

![bg map with train lines](https://www.dropbox.com/s/7gxqjiaamvsg2oj/map_bg_L_with%20color%20lines.png?raw=1)  

On one hand it can be argued that there is more train station accessibility in the more densely populated areas of the city. But considering that the Loop is the epicenter of jobs and the home of big companies in the city, it is a bit problematic that wide swaths of the south side would have more difficulty making it downtown due to the lack of close train stations.  
 

**Bringing It All Together**

Over the course of the two posts, we’ve discussed income, race, population density, crime, businesses, and public transportation. Here are the main takeaways:  
* Chicago is highly segregated by race, where black and white people generally don’t live in the same areas  
* Income is correlated with race – areas that are mostly white have much higher median incomes than areas that are mostly black  
* The north side of the city (not including the farther northwest reaches), which is mostly white is also more densely populated. These areas including the Near North Side, Lincoln Park, Lakeview, etc. also have the highest counts of business licenses in the city, particularly those related to entertainment. These areas also have good CTA L station coverage and high incidences of theft.  
* The south side of the city, which is mostly black, is less densely populated and has less access to CTA L stations. It is largely lacking in business licenses, especially compared to its northern counterparts. When it comes to theft, this area is comparable to many other areas of the city, but has some of the higher incidences of assault and homicide in the city.  
* In the west side of the city, which is largely black, the population density ranges from low to mid-range from block to block. It has some of the highest incidences of homicide and assault. Surprisingly, I would think that an area like Austin with its high crime and low incomes would be lacking in the number of businesses, but Austin has a mid-range level of retail food business licenses compared to the rest of the city. The west side in general has relatively good access to CTA L stations.  
* There is an area of the city, the lower west side stretching out and down to West Lawn, that seems to be a bit more diverse, where it isn’t mostly white or mostly black. The incomes range from low to high-mid, and there is some CTA L coverage, although not a ton.  

Below you can see how variables from the different data categories interact with one another.  

![corrplot](https://www.dropbox.com/s/f4ijjq02siawwf4/corrplot.png?raw=1)

As we move into the final stage of this project, one thing to keep in mind is that even though we can make large generalizations about different neighborhoods in the city, Chicago does vary from block to block. Part III will focus on grouping similar block groups throughout the city, so that an individual would be able to identify blocks that best suit their living preferences.  
Again, feel free to check out my code on [github][github-chi1].



Sources:   
[https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Community-Areas-current-/cauq-8yn6][city of chicago]    
[https://www.census.gov/cgi-bin/geo/shapefiles/index.php][census]  
2017 American Community Survey Data:  [https://www.nhgis.org][nhgis]  
[https://data.cityofchicago.org/Community-Economic-Development/Business-Licenses-Current-Active/uupf-x98q][biz-lic]
[https://data.cityofchicago.org/Public-Safety/Crimes-Map/dfnk-7re6][crime]
[https://data.cityofchicago.org/Transportation/CTA-System-Information-List-of-L-Stops/8pix-ypme][cta]



[github-chi1]: https://github.com/ljshores/Exploring_Chicago
[city of chicago]: https://data.cityofchicago.org/Facilities-Geographic-Boundaries/Boundaries-Community-Areas-current-/cauq-8yn6
[census]: https://www.census.gov/cgi-bin/geo/shapefiles/index.php
[nhgis]: https://www.nhgis.org
[biz-lic]: https://data.cityofchicago.org/Community-Economic-Development/Business-Licenses-Current-Active/uupf-x98q
[crime]: https://data.cityofchicago.org/Public-Safety/Crimes-Map/dfnk-7re6
[cta]: https://data.cityofchicago.org/Transportation/CTA-System-Information-List-of-L-Stops/8pix-ypme