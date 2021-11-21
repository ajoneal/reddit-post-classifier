# Reddit - Premier League vs. Tomorrowland

---

### Project Description

The goal of this project was to create models that would accurately predict between two different subreddits.  My choice of subreddits were thoes of two groups of passionate fan-bases: the football/soccer-crazed fans of the Premier League in England and the EDM/rave/festival fanatics of Belgium's Tomorrowland festival.  My goal was to determine whether the title of a post, the selftext within that post, or a combination of the two would be the best information to feed a model to help in predict which subreddit the post came from.

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
|length|*integer*|total number of individual characters in a title/selftext/post|
|word_count|*integer*|total number of words in a title/selftext/post|

---

### Cleaning

The cleaning of the data was kept very simple as I wanted to keep each post to as close to how it appeared on the website of each subreddit.  Therefore, the simplest fix for imputing the null values was to fill them with a blank string.  However, I did first check that each subreddit had about the same amount of null values before doing so.  The Tomorrowland subreddit had 451 null values in the selftext and the Premier League subreddit had 434 nulls.  It wasn't an exact 50/50 split but was close enough for a simple cleaning of the data.

---

### Preprocessing and EDA