Description: Break the Comma Separated Valued (CSV) file data.csv in the /home/admin/ directory into exactly 10 smaller files of about the same size named data-00.csv, data-01.csv, ... , data-09.csv files in the same directory. All the files should have the same header (first line with column names) as data.csv. None of the smaller files should be bigger than 32KB.

Note: to simplify, disregard broken lines in your files (ie, you can break a file at any point, not just at a newline). The resulting files don't have to be proper CSV files.


Solution: 


1. split -d -n 10 data.csv data-

This splits the data.csv file into 10 different files with the 'data-' prefix --> data-01, data-02 ...

2. But the column headers are absent in all files except data-00, so we copy the column headers into a file and iteratively add it to the other files. 

head -1 data.csv > columns.txt 

for i in {0..9}; do cat columns.txt data-0$i > data-0$i.csv; done 
