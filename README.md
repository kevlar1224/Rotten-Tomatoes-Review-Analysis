# Rotten-Tomatoes-Review-Analysis


This was my contribution to a team final project for one my classes in the UC Davis MSBA program. The assignment was to create a business initiative in which we would use analytics to create a small startup. Our team's idea was to create a consultancy firm that would help streaming services like Netflix. Of course, we didn't have Netflix user data or any streaming service's user data, so we used [a dataset of one million Rotten Tomatoes reviews](https://www.kaggle.com/stefanoleone992/rotten-tomatoes-movies-and-critic-reviews-dataset?select=rotten_tomatoes_movies.csv) to build our proof-of-concept.

We focused on helping Netflix, as it's still the most well-known and well-established streaming service. We identified that Netflix's main issue has been its massive overspending on acquiring content. They've also greenlit sequels to original content before the content even releases, as they want to get production started as quickly as possible.

So for my part of the analytics, I wanted to see if we could predict a streaming property's popularity by its performance early on. I used linear regression and random forest regression to try to predict a movie's popularity based on its early performance.

Due to the large size of the dataset, I used PySpark on Google Colab to clean and analyze the data.

**Analyzing Movies Over Time**

I started with three main kinds of models:
 - A model that predicted the total number of reviews based on the reviews in the first month. The point of this model was to help Netflix identify popular original content to inform their decisions for sequels or related content, using the Rotten Tomatoes reviews as proxies for Netflix user ratings. The most powerful predictors were the number of positive reviews and the number of negative reviews, which allowed us to create a regression model that had an out-ot-sample $R^2$ of 0.85.
 - A model that predicted the total number of reviews a movie will get after it starts streaming, based on total positive and negative reviews by the end of the first month after its theatrical release and all the positive and negative reviews just before they started streaming. This model was meant to help Netflix identify movies that may perform well on their platform, and it treated the Rotten Tomatoes reviews as just internet reviews and not a proxy for Netflix ratings (as). Even with all the information up to the month just before each movie started streaming, the model only had an out-of-sample $R^2$ of about 0.65. 
 - A model that predicted the change in monthly reviews when a movie starts streaming. This model was similar to the second, but rather tha predict the total number of reviews after the streaming release, it predicted how many more or less reviews a movie receives when it started streaming compared to the month just before it started streaming. This model only had an out-of-sample $R^2$ of about 0.28.

I also created a fourth model, which was a sort of hybrid of the first two models. By again treating the Rotten Tomatoes dataset as a representation of online reviews (and not as a proxy for Netflix ratings), I was able to use all the positive and negative reviews up until the end of the first month after release (including reviews before the official release, which account for about 25% of all reviews) and use sentiment analysis on the review text to predict the total number of reviews. This created a model with an out-of-sample $R^2$ of about 0.94. This model allows streaming services and production companies to accurately predict a movie's popularity - and therefore its profitability - based on online reviews and within 30 days after the movie is released.

**Topic Modeling on Reviews by Genre**

I also spent some time exploring the use of natural language processing (NLP), specifically topic modeling, to identify features that people liked to see in movies. I focused on the most popular genres of movies and separated the positive and negative reviews to differentiate between good features and bad features. I used the Spark NLP library and was able to identify topics for the different genres, but decided that the results weren't very interesting. I've included this notebook to serve as a reference for anyone to use, even though similar references already exist.
