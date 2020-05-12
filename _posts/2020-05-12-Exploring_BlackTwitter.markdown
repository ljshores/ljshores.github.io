---
layout: post
title:  "Exploring BlackTwitter"
date:   2020-05-12
categories: python text_analysis
---
Have you heard of BlackTwitter? If you know me, you know that I’m a bit slow when it comes to social media. But I am a black woman and try to stay down with the culture. So my understanding of BlackTwitter has been that it’s when black folks bring our collective voice to the platform to discuss something. But I wasn’t sure if this collective voice had some structure, i.e. if it lived under a black twitter hashtag. So I set out to answer that question… Can analyzing tweets with variations of the hashtag “blacktwitter” give us a view into a black collective voice? And if so, what is it saying?

To go about answering these questions, I used Twitter’s Search api to pull tweets with variations of the hashtag #BlackTwitter. The api will only allow you to pull data from the last seven days, and it will not pull an exhaustive list of all tweets. I created a loop and used tweepy to pull a certain amount of tweets, pause, and continue to pull more tweets. Here's a sample of the data.  

![dfsample](https://www.dropbox.com/s/1t2m92ympk9dqst/df_sample.png?raw=1)

This exercise yielded ~37K tweets, but when I removed duplicate text I was left with just 620 tweets. This was a bit alarming to me, because I wasn’t sure why I was yielding so many duplicates. Was something wrong with my pull methodology? Was I pulling a bunch of retweets? While a check of unique twitter id’s showed that there were duplicated tweet text that had unique id’s, this nowhere near accounted for most of the duplicates. For the sake of answering the posed question, I decided to move forward with the analysis on the de-duped data rather than do more digging into why there were so few unique tweets.


**Exploring the Data**

The tweets were collected from April 25 through May 9. The majority of the tweets come from various parts of the US, but there were a noticeable amount of tweets from Pakistan and India. This was interesting to me, so I spot checked tweets coming from these places and found that the hashtag seemed to be used a lot in reference to clothing/fashion that was the color black. This led me to question – Twitter is a global platform; how do we reconcile hashtags that may be geared towards a certain movement in a certain place, and the fact that other places may not be aware of that movement.  

![location](https://www.dropbox.com/s/pajg9h8l4826006/location_barplot.png?raw=1)


I created a word cloud to get a quick view of most frequent words.

![wordcloud](https://www.dropbox.com/s/c26y77juvrk8hy2/word_cloud.png?raw=1) 


I also took a look at what were the most frequent hashtags in this corpus of tweets. Of course, we expect “blacktwitter” to be there a lot, so I removed it. At the time that I was pulling tweets, information and video about the lynching of Ahmaud Arbery, a black runner in Georgia, had surfaced. So I expected to see a lot of commentary on that subject. Looking at the top 30 most frequent hashtags I saw that the Arbery topic manifested itself in several different hashtags. Black excellence, racism, and COVID19 were other top tags. On the other end of the spectrum, hashtags such as BlueTwitter and RedTwitter occurred, which indicate posts that may be those that were geared towards fashion in other countries. It was also interesting that there were many hashtags of different countries, which indicates either the globalized use of this hashtag or the global relevance.

![hashtagwordcloud](https://www.dropbox.com/s/w1ee14beku8n4lc/hashtag_wordcloud.png?raw=1)


**Grouping Tweets**

The last thing I wanted to do was get a better grasp of the main topics within the text. In a situation like this, I would have liked to use a method like Latent Dirichlet Allocation for topic modeling. But knowing that we had so few tweets, it just didn’t seem appropriate. Therefore, I decided to do a hierarchical clustering and check the groups to see if any obvious themes emerged. I converted the cleaned twitter text to word embeddings using Word2Vec. The spatially visualized embeddings seemed very clumped together. I believe this is again perhaps the result of too few observations, and a very small amount of words in each observation, which would cause all the words to seem close.    

![Embeddings](https://www.dropbox.com/s/bqzn1ut2w6o2p9n/embeddings_pic.png?raw=1)


I proceeded to cluster the embedded sentences using hierarchical clustering. To evaluate I looked at how many observations fell into each of the four clusters, and to try to make sense of the clusters I looked at most frequent words and highest tf-idf weights per cluster. Neither of these methods yielded much insight into a unique topic or group composition.   

If you'd like more details about the analysis and the code, please check out my [github repo] [github-blacktwitter].


**Final Thoughts**

From the limited amount of data we had to work with, I get the sense that the blacktwitter hashtag is not a great representation of a collective of black voices on Twitter. I get the sense that although major topics here included black excellence, racism, and current issues facing black people, a broader idea of what black twitter really is cannot be captured under one hashtag. This is evidenced by the array of other hashtags that were used in conjunction with #BlackTwitter. Also, using this hashtag as a representation can be difficult because there are trolls using it in very negative ways, and there are people using the hashtag that may not have the social context of Black people, particularly in the US.   

Of course, we have to remember that this is a very small sample of the usage of the hashtag. In the future, finding a way to pull more tweets over a large amount of time would give us a broader view of how the tag is used, and how usage coincides with certain major events. With more data, we could do a more useful exploration of topic modeling. For now, my sense is that if you really want to understand black twitter, you just have to keep your eyes and ears open; it may manifest itself under a neat hashtag and on the other hand it may not.   



[github-blacktwitter]: https://github.com/ljshores/Explore_BlackTwitter

