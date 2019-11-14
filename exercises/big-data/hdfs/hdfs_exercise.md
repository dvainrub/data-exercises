# Setup HDFS Docker


## Pre-requisites
##### 1. Download [Docker](https://docs.docker.com/v17.09/engine/installation/).
##### 2. Pull and run [Hadoop's Docker Image](https://hub.docker.com/r/sequenceiq/hadoop-docker/):
```bash
# Open the bash shell and run:
docker pull sequenceiq/hadoop-docker
docker run -it sequenceiq/hadoop-docker:2.7.0 /etc/bootstrap.sh -bash

# Run the following command to test the installation (inside the docker bash)
cd $HADOOP_PREFIX
bin/hdfs dfs -ls /  # It should print all the folders in root, '/user' in this case
```

# Exercises
As you already know, HDFS is a distributed filesystem.
As a FS, it comes with a CLI (Commands-line interface) that allows you to do many things like:
- List all files in a directory
- Read files
- Copy and move files
- Copy files into and from your local FS into the HDFS
- And many others

In this exercise we will upload a file into the HDFS and play with the CLI.

You can take a look at the [documentation](https://hadoop.apache.org/docs/r2.4.1/hadoop-project-dist/hadoop-common/FileSystemShell.html) to check the available commands, or just run
`bin/hdfs dfs -help`    

#### Exercise 1 - Download the [MovieLens Dataset](https://grouplens.org/datasets/movielens/)
1. Create a directory inside the folder `/user/root` in HDFS and call it `movie-lens` (Hint: use `mkdir`)

2. Copy the MovieLens Dataset to the Docker container
```bash
docker cp [ml-latest-small path] $(docker ps -q):/usr/local/hadoop/
docker cp ~/Desktop/Bootcamp/datasets/ml-latest-small/ $(docker ps -q):/usr/local/hadoop/
```

. 2. Download the MovieLens dataset by running:
```bash
curl -SOL http://files.grouplens.org/datasets/movielens/ml-latest-small.zip
unzip ml-latest-small.zip
rm -f ml-latest-small.zip

# You can list all the files downloaded
ls ml-latest-small

# And take a look at the files
cat ml-latest-small/movies.csv 
```

#### Exercise 2 - Upload the dataset to HDFS and apply some commands
1. Upload the `ml-latest-small` folder into the folder `/user/root` inside the HDFS

The following steps should be run inside the HDFS
1. List all the files inside `ml-latest-small`
2. Read the `README.txt` file
3. Copy the `links.csv` file into a new file named `links_my_copy.csv` in the same directory
4. Delete the file you just created: `links_my_copy.csv`
5. Create a new file called `empty_file.txt` inside the folder `/user/root`
6. Rename the `movie-lens` folder with a new name: `movie-lens-dataset`
7. Copy `ratings.csv` to your local FS


#### Exercise 3  (Advance) - Analyze the HDFS 
1. Move every file **inside** `ml-latest-small` into `movie-lens-dataset`

        `ml-latest-small` should be empty
        `movie-lens-dataset` should contain the files: 
        'README.txt', 'empty_file.txt', 'links.csv', 'movies.csv', 'ratings.csv', 'tags.csv'   

Answer the following questions by applying the necessary commands:
2. What's the size of each folder inside `/user/root`? What's the size in KBs/MBs (a readable format)?
3. What's the amount of lines in the file `README.txt`? (Hint: You'll need to mix HDFS and linux commands)