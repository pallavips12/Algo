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
 

#Import text data
tweets<-read.csv("bitcoin_tweets.csv",stringsAsFactors = FALSE)
# view structure of tweets
str(tweets)
nrow(tweets)
#isolate text from tweets
bitcoin_tweets<-tweets$text
bitcoin_tweets

#corpus - is a collection of documents
library(tm)
bitcoin_source<-VectorSource(bitcoin_tweets)
bitcoin_corpus[[15]][1]
#creating a corpus
bitcoin_corpus<-VCorpus(bitcoin_source)
bitcoin_corpus
# print the content of the 15th tweet
bitcoin_corpus[[15]][1]
bitcoin_corpus[[15]]

#preprocessing functions
#tolower(), removePunctuation(), removeNumbers(),stripWhiteSpace(),removeWords(# removes specific defined words)
#cleaning with qdap 
#bracketX,replace_number,replace_abbreviation, replace_contraction, replace_symbol
#stop words - tm package offers 174 stop words

# using c() function more mords can be added to stopwords list
#all_stops<-c("word1","word2",stopwords("en"))
#once the list is ready you can use removeWords()
#removeWords() takes two arguments - text object to which it is applied to and list to remove
removeWords(bitcoin_tweets,stopwords("en"))
new_stops<-c("bitcoin","crypto",stopwords(("en")))
data<-removeWords(bitcoin_tweets,new_stops)

