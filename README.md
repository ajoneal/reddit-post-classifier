# Reddit - Predicting Premier League vs. Tomorrowland

---

### Project Description

The goal of this project was to create classification models that would accurately predict between two different subreddits.  My choice of subreddits were thoes of two groups of passionate fan-bases: the football/soccer-crazed fans of the Premier League in England and the EDM/rave/festival fanatics of Belgium's Tomorrowland festival.  My goal was to determine whether the title of a post, the selftext within that post, or a combination of the two would be the best information to feed a model to help in predict which subreddit the post came from.  To do this I created a different notebook to examine each of these different features that I would feed my models with.

---

### Data

The data for this project was pulled using Pushshift's API to pull data from the Premier League and Tomorrowland subreddits.

* [Premier League Subreddit](https://www.reddit.com/r/PremierLeague/)
* [Tomorrowland Subreddit](https://www.reddit.com/r/Tomorrowland/)

|Feature|Type|Description|
|---|---|---|
|title|*string*|the title of a specific post in a subreddit|
|selftext|*string*|the text within a specific post in a subreddit|
|subreddit|*string*|the name of the subreddit a post came from|
|created_utc|*integer*|numeric timestamp for when the post was created|
|post_text|*string*|combination of the title and selftext columns to examine the entire post from a subreddit|
|length|*integer*|total number of individual characters in a title/selftext/post|
|word_count|*integer*|total number of words in a title/selftext/post|

---

### Cleaning

The cleaning of the data was kept very simple as I wanted to keep each post to as close to how it appeared on the website of each subreddit.  Therefore, the simplest fix for imputing the null values was to fill them with a blank string.  However, I did first check that each subreddit had about the same amount of null values before doing so.  The Tomorrowland subreddit had 451 null values in the selftext and the Premier League subreddit had 434 nulls.  It wasn't an exact 50/50 split but was close enough for a simple cleaning of the data.

---

### Preprocessing and EDA

When examining the data, I looked at the total character counts and word counts in the titles, selftexts, and posts.  Premier League titles were longer on average than Tomorrowland titles and Tomorrowland selftexts were longer on average than Premier League selftexts.  There didn't seem to be a very clear separation on the entire post's character length or word counts.  The entire posts had the longest character lengths and word counts on average, then the selftexts, and finally the titles.  I suspected that the most accurate predictions would come from the entire posts, then the selftexts, then the least accurate would be the title based on this believing that the more information the model was given the more accurate it would be.

I then used a countvectorizer to separate the words in the feature columns of each notebook.  I looked at the most common words from each subreddit.  For the titles, there was a little bit but did not seem to be much overlap of top words from one subreddit title to the other.  This should benefit the models, helping them predict more accurately.  There was a lot more overlap in the selftexts and entire posts between the two subreddits which led me to believe there would be more errors in the models due to this (especially in the selftext notebook because that had the most overlap).  Also, the amount of empty values in the selftexts looked to be an issue for predicting subreddits for the models.  Although it was an almost 50/50 split, the lack of data in those cells could pose a problem for the models.

---

### Modeling and Analysis

For each notebook, I created four different models for each feature that I would feed the models.  The Premier League subreddit was set as the positive target and the baseline accuracy for each model to beat was 50%.  For each of the four models, I tried each of them with a countvectorizer and a tfidfvectorizer to see if either had an effect on the accuracy of each model.  There did not seem to be much difference when using one or the other for all three notebooks (scoring words vs. counting them had little to no effect).  All models were also GridSearched, slightly tweaking parameters, to optimize accuracy for each individual model.  For all three notebooks, the logistic regression model with the tfidfvectorizer was the the model that predicted most accurately and the KNN model with countvectorizer was the least accurate in predicting the correct subreddit.  In 22 out of the 24 models I created, the Tomorrowland subreddit was predicted more often than the Premier League subreddit.  This led to higher specifities for these models and lower sensitivities.  The two models that did not fall into this pattern were the KNN models with the tfidfvectorizer in the title and selftext notebooks.  These two models predicted the Premier League subreddit much more often than the Tomorrowland subreddit and had higher sensitivities than specificities.

After reviewing the confusion matrices for the models, I began to look at where the models were failing and what some of the reasons for incorrect predictions were.  In all three notebooks, several of the incorrect predictions seemed to come from some of the overlap of top occuring words in each subreddit.  This was more prevalent in the title notebook than the selftext and post notebooks.  In the selftext and post notebooks, a majority of the incorrect predictions came from deleted, removed, or empty selftext cells.  This also led to lower accuracies from the models created based on the selftext.  Although the selftexts on average had longer lengths and word counts than the titles and more data in the cells that weren't empty, those cells that were empty/deleted/removed seemingly decreased the accuracy of the models compared to the models created based on the titles.  I also reviewed the prediction probabilities in all the models and the probabilities for the selftext models and several more that were close to the 50% mark.  This was most likely due to the amount of empty/deleted/removed cells in the selftext.  The models that were given the entire post were the most accurate models overall.  However, several of the incorrect predictions in those models came from the empty/deleted/removed selftext portion of the post that made up part of that feature.

### Conclusion and Recommendation

Given two subreddits, the best way to create a model for predicting which subreddit a post comes from would be to give it both the title and selftext information to help it predict which subreddit that post came from.  Some subreddits do not have much in the selftext of a post but at least some information can be gained from the title.  Therefore I would recommend creating a model based on the entire post and not just the title or selftext and even stacking a few models would help create even more accurate predictions possibly.

### Presentation Link