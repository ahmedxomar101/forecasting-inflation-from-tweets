# forecasting-inflation-from-tweets
In this project, I extracted +40 leading indicators to forecast the UK inflation rate from Twitter tweets from 2018 to 2022 in the UK.

These efforts are part of my work for the Data-Driven Economics course in my master's at Sapienza University.
## Intro
Here we have all tweets posted in the UK for the period 2018 to 2022 and the task is to extract leading indicators and signals out of these tweets to forecast the UK inflation rate during that period. We did so with very high performance with the proper feature engineering that yield in extracting the proper indicators.
## Data
The data is available at the following [link](https://drive.google.com/file/d/1uDACTehGNzQUAsBmLQeAxYf1le1ONPbK/view?usp=sharing).

Data Attributes Description:
* |-- id: integer (nullable = false) (hashed id)
* |-- verb: string (nullable = true) (can be post or share if a RT)
* |-- user: integer (nullable = false) (hashed user id)
* |-- inreplyto: struct (nullable = true) (in reply to)
    * |-- link: string (nullable = true)
* |-- link: string (nullable = true)
* |-- body: string (nullable = true) (body of tweet)
* |-- retweetbody: string (nullable = true) (body of retweeted tweet)
* |-- date: string (nullable = true) (date)
* |-- postedtime: string (nullable = true) (date and time)
* |-- retweetcount: long (nullable = true) (number of RT)
* |-- favoritescount: long (nullable = true) (number of likes)
* |-- generator: string (nullable = true) (generator)
* |-- twitter_lang: string (nullable = true) (language)
* |-- year: string (nullable = true) (year)
* |-- userLocation: string (nullable = true) (user location)
* |-- userFriends: long (nullable = true) (user friends)
* |-- userFollowers: long (nullable = true) (user followers)
* |-- userNumTweets: long (nullable = true) (number of tweets)
* |-- userVerified: boolean (nullable = true) (verified)
* |-- userLanguage: string (nullable = true) (user language)
* |-- userBio: string (nullable = true) (user bio)
* |-- country: string (nullable = true) (country)
* |-- countrycode: string (nullable = true) (country code)
* |-- locality: string (nullable = true) (locality)
* |-- region: string (nullable = true) (region)
* |-- subregion: string (nullable = true) (sub region)
* |-- locationname: string (nullable = true) (location name)
## Code
Available in the following notebook, everything is divided into sections and sub-section for ease of navigation:
* [Notebook](https://github.com/ahmedxomar101/forecasting-inflation-from-tweets/blob/master/DDE%20Course%20-%20Forecasting%20Inflation%20from%20Tweets%20-%20Ahmed.ipynb).
* [HTML](https://github.com/ahmedxomar101/forecasting-inflation-from-tweets/blob/master/DDE%20Course%20-%20Forecasting%20Inflation%20from%20Tweets%20-%20Ahmed.html) version of the notebook.
## Results
After performing many trials, I have identified two models that can forecast inflation with great performance which is 92.5% and 97.6% better than the baseline of my experiments. 

All the forecasting made is by using 48 months of inflation rate for training (equivalent to 4 years) and forecasting 12 months in one shot.
1. **ARIMA (Baseline)**, optimal ARIMA Model is (1,1,1)
    * MSE = 4.67
    
      ![image](https://github.com/ahmedxomar101/forecasting-inflation-from-tweets/blob/master/assets/ARIMA_base.png)
2. **Linear Regression**
    * MSE = 0.35
    * Indicators used: ‘countOfAllTweets', 'sumOfallTweetsTop15Unigrams’
    * Lags used: first and fifth.

      ![image](https://github.com/ahmedxomar101/forecasting-inflation-from-tweets/blob/master/assets/LinearRegression_2lags_2sginals.png)
3. **VAR**
    * MSE = 0.11
    * Indicators used: ‘countOfInflationTweets', 'sumOf+veSentimentForAllTweets', 'sumOf-veSentimentForInflationTweets', 'meanOfinflationTweetsTop15Bigrams'
    * Lags order: 4
    
      ![image](https://github.com/ahmedxomar101/forecasting-inflation-from-tweets/blob/master/assets/VAR_4lags_4signals.png)

**Extra**: 

  * Here is a screenshot of the correlation between the inflation rate and the indicators extracted in the feature engineering process of the tweets.

    ![image](https://github.com/ahmedxomar101/forecasting-inflation-from-tweets/blob/master/assets/correlation_betInflRate_andIndicators.png)
