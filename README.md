# The Great NLP Bake Off

One of my not-so-secret obsessions is the British television show, the Great British Bake Off or as I like to call it, GBBO. Being an avid baker myself, it’s so entertaining and mesmerizing to see all of these amazing home bakers make these amazing creations from scratch. The show is such a stark contrast to American competition shows because of how pleasant and supportive all of the contestants are to one another. There are never any insults or shit talking, just a lot of encouragement and, sometimes, consoling when a contestant is feeling down. Their relationships and the relationships between the contestants and the hosts and judges are some of my favorite parts of the show. It’s also a great show to wind down to after a stressful day. 

With this in mind, I wanted to see what insights and trends I could get from the dialogue throughout the seasons, including what topics recurred over the seasons/episodes, if there was a way to determine what flavors tended to relate to one another, and if I could use sentiment analysis as well as topic modeling to see if these would corroborate my thoughts on the show and to uncover some trends over the seasons. 

## Data

To do my analysis, I decided to use the subtitles for the first four seasons of GBBO that are available on Netflix which ended up being 40 episodes in total. I chose the first four seasons, seasons 1 through 4, to keep some consistency but also because I have a bias towards the original judges and hosts of the show, Mary Berry, Mel and Sue. Seasons 5 and 6 have a new judge who joined Paul Hollywood, one of the original judges and two new hosts hosts. 

Using Netflix, I downloaded the subtitles for all of the episodes from these seasons in VTT files and parsed each file and created a list of dictionaries organized by episode and text. Using the list of dictionaries, I, then, created a DataFrame.

## Text Pre-Processing

To achieve what I want to do with all of the subtitles, I had to separate each episode into individual dialogue by speaker using RegEx. (For more information on how I did this, check my Jupyter Notebook) 

Once I had speaker and dialogue separated, I used the SpaCy library to lemmatize words, to remove stop words and to tokenize the dialogue. I then used scikit-learn’s TF-IDF implementation to create a matrix of each dialogue’s word frequency vector. I chose TF-IDF over other vectorizers because it took into account the word count disparities as the dialogue for certain people and in certain episodes were shorter or longer than others. For more information on how I pre-processed, check out my Part 2 notebook.


## Modeling

### Topic Modeling
To do my topic modeling, I used Non-Negative Matrix Factorization as it gave me the most sensible topics. After playing around with the topics and groupings, I landed on 8 topics:

![](https://paper-attachments.dropbox.com/s_9A3FB326D705C9517993DA8D5383D9EA2E1AEB61E232E1B0B68575E32746A8F8_1564107287020_image.png)


### Word2Vec
I then used gensim’s Word2Vec to create word vectors to find word clusters that are most similar to one another. I did this to see which words were most similar to each other in hopes of seeing whether certain flavors appeared with certain baked goods. 

### Sentiment Analysis with Vader 
To gain further insights, I used Vader for sentiment analysis over all of the seasons. I used this to compare the sentiment over each of the contestants over the seasons as well as the judges to see whether there were any trends in whether either judge was more negative or positive than the other. 

## Results

### Topic Modeling
From my topic modeling, it made sense that each episode incorporated all 8 of the topics. What was more interesting was the makeup of each episode of each topic. 

![](https://github.com/amyksu/great-nlp-bake-off/blob/master/visuals/topics.gif)

The topic make ups often correlated to the challenge of the week. For example, looking above, the darker brown represents the bread topic and the episodes where there is a greater percentage of the bread topic were the weeks where it was a bread challenge. In addition, the light pink represents the ingredients topic and in episode 305, there is a large percentage of that topic because it was “Alternative Ingredients” week. 

### Word2Vec

To show the results of my pre-trained Word2Vec embedding, I used TSNE to plot a subset of similar words. I applied TSNE to the matrix to project each word to perform dimensionality reduction to present the words in a 2D space. The subset of words I chose were:

- Cake
- Pie
- Pastry
- Eggs
- Bread
- Winner
- Raspberry
- Technical
- Chocolate

![](https://paper-attachments.dropbox.com/s_9A3FB326D705C9517993DA8D5383D9EA2E1AEB61E232E1B0B68575E32746A8F8_1564175230227_image.png)


Based on the above, the main takeaways were:

   - The word “winner” is most similar to “bread” and “technical” which, as a devoted fan of the show, is true as most winners are good at technicals and usually win bread week. 
   - The word cake is most similar to the flavors “chocolate” and “raspberry”. 
   - The words “pie”, “pastry”, and “egg” are most similar and closest to each other which makes sense because a lot of the pie crusts made by the bakers are pastry crusts. In addition, it makes sense that eggs are close to both words as eggs are used for pastry and pie crusts to give them the shiny brown crispy look. 

### Sentiment Analysis
From my sentiment analysis, I plotted the overall sentiment by episode between the male and female judges and contestants. When looking at the average, it’s hard to see an overall trend.

![](https://github.com/amyksu/great-nlp-bake-off/blob/master/visuals/Sentiment.gif)


However, when looking at the individual sentiments, in the second and fourth seasons, the males were more negative than the females. In the first and third seasons, it was the opposite. This is further supported when looking at the individual positive sentiment. When it comes to the judges, Mary was more positive than Paul in most of the seasons up until the fourth season. 

## Future Work

In the future, I would love to delve deeper into seeing if there was a way to predict which flavors tend to yield more positive judging from the judges and whether I can predict what flavors will win. Overall, I would like to focus more on the actual baking on the show and get more information on the ingredients and the baking on the show. 
