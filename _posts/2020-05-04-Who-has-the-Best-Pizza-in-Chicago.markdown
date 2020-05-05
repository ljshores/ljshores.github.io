---
layout: post
title:  "Who Has the Best Pizza in Chicago"
date:   2020-05-04
categories: fun_analysis tableau python
---
As I mentioned before, I love Chicago. One of the reasons is that the city has AMAZING food, and I LOVE to eat! A heated topic among any Chicagoan is who serves up the best pizza. So one summer I decided that I would try to use data to figure this out. This analysis is a two parter. 

**Part I: My Summer of Pizza**  
In the first part, my bf at the time and I visited twenty pizzerias and assigned them a score out of 10 for each of four categories: toppings, crust, sauce, and an overall score. Being that there were two of us that makes for 20 possible points for each category and a total possible score of 80 points for a pizza.

I made a visualization of all our results in [tableau][tableau-pizza] which you can take a look at. Spoiler alert: Pequod’s had the best deep dish pizza and Home Run Inn had our favorite thin pizza.

**Part II:**  
In part II, I scraped data from yelp for the restaurants in question and did some digging to try to figure out what other people liked and why. You can see the full analysis code on my [github][github-pizza].

I scraped reviews from Yelp and used Beautiful Soup in python to parse the data, getting fields for rating, post date, and review description. I ran some quick summary statistics to get a sense of what was going on with the reviews. We see the top restaurants in terms of average rating and we also see that some of these pizzerias have a ton of reviews, while others have very few.

![summary stats](https://www.dropbox.com/s/h6xv12kag0wyl5x/summary_stas.png?raw=1) 


Restaurants aren’t static entities, so I wanted to take a look at the average ratings over time. We see that restaurants like Benny’s and Paisan’s had sharp declines in some years, while places like Freddy’s stayed pretty consistent. 

![ratings time](https://www.dropbox.com/s/kj1ydjxkv7yv1le/ratings_time.png?raw=1) 

Looking at the number of reviews over time revealed places like Bennys and Paisan’s had very few reviews during their rough years, which means that a single low score could have a bigger impact on the overall score for that year. Pequod’s and Piece had more reviewers in leaps and bounds over the years, which is why they skyrocketed off the chart. In general most restaurants saw an increase in reviewers, which may be more a reflection on changing behavior in society (the tendency to go online and leave reviews) rather than any specific thing about the restaurant. But also, the number of reviewers could be a reflection of “buzz”. The more people say something is good, the more people want to go try it.

![reviews time](https://www.dropbox.com/s/sb49kxczhb3a64j/review_cnt_time.png?raw=1)

Below I plot the relationship between number of reviews and ratings.

![cnt v rate](https://www.dropbox.com/s/gfbg73x2fco6pj9/cnt%20vs%20ratings.png?raw=1) 

In general there seems to be a positive relationship, but outliers Piece and Pequod’s show that having the most reviews doesn’t mean most highly rated, and Dante’s and Benny’s shows that low number of reviews doesn’t mean low ratings.

The last portion of the analysis I want to talk about is digging into the text descriptions. I looked at ngrams of the text to see what sequence of words occurred most frequently for some restaurants. Trigrams were interesting because I was able to discern specific characteristics about the pizza like Spacca Napoli is good for Neopolitan pizza, and Dante’s is a New York style pizza. People like Pequod’s and Lou Malnati’s for their deep dish, while Benny’s seems to be a place people like to order in for. I also was able to see that Freddy’s which had the highest average rating had many mentions about things that weren’t related to pizza, like “Italian ice” and “Italian food”, which make me question if their high rating was even driven by pizza.

In short, the yelp reviews did not really line up with my [“Summer of Pizza”] [tableau-pizza] favorites. The pizzas that we liked best didn’t register the top ratings on Yelp. And the Yelp reviews showed that popularity doesn’t necessarily equate to high opinions. I know everyone has strong opinions about what they think is the best. But I believe it really depends on what you grew up liking and what characteristics are most important to you in a pizza. I personally think a great crust and the right amount of sauce is key. So maybe we just have to agree to disagree (for all you Lou Malnati’s fans, I really disliked that pizza).

If you’re interested, here are the pizzas we tried ranked from our favorite to least favorite next to Yelp’s rank of top average rating and bottom average rating. Note, that I seemed to have missed three restaurants in the Yelp analysis. My apologies.

 
![myRank v Yelp](https://www.dropbox.com/s/ix21p27ahwlxzcw/my_ranking_v_yelp.png?raw=1)






[tableau-pizza]: https://public.tableau.com/profile/lauren.shores#!/vizhome/ChicagoPizzaTour/Dashboard1

[github-pizza]: https://github.com/ljshores/Chicago-Summer-of-Pizza

