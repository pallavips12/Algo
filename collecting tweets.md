#scrapping tweets for bitcoins using r
install.packages("bit64")
install.packages("twitteR")
install.packages("ROAuth")
library("twitteR")
library("ROAuth")

#Set the working directory
setwd("D:/ML class")
getwd()

api_key <- "OmdK90LrAmxRgJUqe3Jw2lbOq"
api_secret <- "scFt16snW9QgfO2sPN8yR1AInlEAxj02zR2YtSEozUQOZ6vI1r"
access_token <- "949315530938200064-4b1GIro58LU4nWPefmnIrgDh3wkmB0K"
access_token_secret <- "SntWz2t5rwpi4OOkniUN0A8CjE1OPDobrGx49adjdNAi9"

setup_twitter_oauth(api_key,api_secret,access_token,access_token_secret)
bitcoin_tweets <- userTimeline("BTCTN", n = 2000)
#n = number of tweets
bitcoin_tweets_df <- twListToDF(bitcoin_tweets)
dim(bitcoin_tweets_df)
View(bitcoin_tweets_df)

write.csv(bitcoin_tweets_df,file=paste("bitcoin_tweets.csv"))

bitcoin_tweets_df<-read.csv("bitcoin_tweets.csv",stringsAsFactors = FALSE)

View(bitcoin_tweets_df)

library(tm)
bitcoin_source<-VectorSource(bitcoin_tweets_df)
bitcoin_corpus<-VCorpus(bitcoin_source)
bitcoin_corpus
bitcoin_corpus[[2]]
bitcoin_corpus[[2]][2]
