# Setup HDFS Docker

# Exercises - Solution
#### Exercise 1 - Download
```bash
# 1
bin/hdfs -mkdir /user/root/movie-lens
bin/hdfs -mkdir movie-lens

# 2
mkdir local-data
```

#### Exercise 2 - Upload and play
```bash
# 1
bin/hdfs dfs -copyFromLocal ml-latest-small /user/root
bin/hdfs dfs -copyFromLocal ml-latest-small .

# 2
bin/hdfs dfs -ls ml-latest-small

# 3
bin/hdfs dfs -cat ml-latest-small/README.txt

# 4
bin/hdfs dfs -cp ml-latest-small/links.csv ml-latest-small/links_my_copy.csv

# 5
bin/hdfs dfs -rm ml-latest-small/links_my_copy.csv

# 6
bin/hdfs dfs -touchz /user/root/empty_file.txt
bin/hdfs dfs -touchz empty_file.txt

# 7
bin/hdfs dfs -mv movie-lens movie-lens-dataset

# 8 
bin/hdfs dfs -copyToLocal movie-lens-dataset/ratings.csv .
```

#### Exercise 3 - Advanced
```bash
# 1
bin/hdfs dfs -mv ml-latest-small/* movie-lens-dataset

# 2
bin/hdfs dfs -du
bin/hdfs dfs -du -h

# 3
bin/hdfs dfs -cat movie-lens-dataset/README.txt | wc -l
# Should return '157'
```
