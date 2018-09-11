all: createFile downloadFile storeHeader storeRest state count column
createFile: 
	touch README.txt
downloadFile:
	curl -O https://raw.githubusercontent.com/fivethirtyeight/data/master/murder_2016/murder_2015_final.csv
storeHeader: downloadFile
	sed -n '1 p' < murder_2015_final.csv > murder_header.csv
storeRest: downloadFile
	sed '1 d' < murder_2015_final.csv > murder_data.csv
state: storeRest
	cat murder_data.csv | grep "Illinois" > murder_illinois.csv 
count: storeRest
	cat murder_data.csv | grep "Maryland" | wc -l > murder_maryland.count 
column: storeRest
	cat murder_illinois.csv | awk -F "," '{print $$3,$$4}' > murder_illinois_2014-2015.csv
clean:
	rm -rf *.csv *.txt *.count
.PHONY: clean all


