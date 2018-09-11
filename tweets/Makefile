all: | clean download prep analyze clean 
.PHONY: all clean
download: clean
	mkdir data
	wget -P data www.derekruths.com/static/reading_tweets/books_tweets100000.txt.gz
	gunzip data/books_tweets100000.txt.gz
prep: download
	cat data/books_tweets100000.txt | jq -r "[.user.id_str, .user.created_at, .user.lang, .text] | @tsv" > book_tweets.tsv
	cat book_tweets.tsv | awk -F "\\t" '$$2 ~ /Oct 23/ {print}' | awk -F "\\t" '$$2 ~ /2012/ {print}' > tweetsOct2012.tsv
	cat book_tweets.tsv | awk -F "\\t" '$$4 ~ /#gameofthrones/ {print}' > tweets_got.tsv
analyze: download
	echo "1.    How many tweets have lang = “ru” (use the Russian language)? " >> results.txt
	cat data/books_tweets100000.txt | jq 'select(.user.lang == "ru") | .id' | wc -l >> results.txt 
	echo "2.    How many tweets are from August 2016? " >> results.txt
	cat data/books_tweets100000.txt | jq 'select(.created_at | contains("Aug") and contains("2016")) | .id' | wc -l >> results.txt
	echo "3.    How many tweets contain a retweet (start with “RT”)? " >> results.txt
	cat data/books_tweets100000.txt | jq -r 'select(.text | startswith("RT")) | .id' | wc -l >> results.txt
	echo "4.    How many tweets mention #gameofthrones? " >> results.txt
	cat data/books_tweets100000.txt | jq -r 'select(.text | contains("#gameofthrones")) | .id' | wc -l >> results.txt
	
clean:
	rm -rf data *.csv *.tsv temp*
