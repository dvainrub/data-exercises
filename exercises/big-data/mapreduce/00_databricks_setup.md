# Setup Databricks

### Create a Databricks Account
1. Go to [databricks.com](https://databricks.com/)
2. Click on `Try Databricks` on the top right corner.
3. Click on `Get Started` under `Community Edition`.
4. Fill in your details and `Sign Up`.
5. Confirm the email you received from Databricks.

### Create your first cluster
1. On the left side bar click on `Clusters -> Create Cluster`.
2. Call your cluster `MR Cluster`.
3. Chose the Runtime Version to be `5.4 (Scala 2.11, Spark 2.4.3)`.
4. Click on `Create Cluster`. Wait until it changes its status from `Pending` to `Running`.
5. Click on the Cluster and then go to the `Libraries` tab on the top.
6. Click on `Install New -> PyPI` and write `mrjob` in the `Package` field. This will add the required Python package to write MapReduce jobs.


### Upload the [MovieLens Dataset](https://grouplens.org/datasets/movielens/) to Databricks
1. Download the [Small Movie Lens Dataset](http://files.grouplens.org/datasets/movielens/ml-latest-small.zip) to your computer.
2. Unzip the downloaded files.
3. On the left side bar click on `Data -> Add Data`.
4. Drop the files inside the `ml-latest-small` folder into the grey block. They will be uploaded into DBFS (Databrick's FileSystem) under the path: `/FileStore/tables/`.


### Create a Notebook inside Databricks
1. On the left side bar click on `databricks -> Create a Blank Notebook`.
2. Call it `MovieLens Exploration`
3. Run the following commands in order to explore the data you just uploaded and get to know Databricks
```
# Show all recently uploaded files
display(dbutils.fs.ls("/FileStore/tables"))

# Print the first rows of the 'movies' file
dbutils.fs.head("/FileStore/tables/movies.csv")

# Create a table from the 'movies' data and show a sample
%sql
CREATE TABLE IF NOT EXISTS movies USING CSV OPTIONS (path "/FileStore/tables/movies.csv", header "true");
SELECT * FROM movies;
```
* Repeat the process above to create and explore the 'ratings.csv' and 'tags.csv' files.
* Try to understand what's all this data, you'll need it for the next exercises. You can read the README.txt file or visit [MovieLens page](http://files.grouplens.org/datasets/movielens/ml-latest-small-README.html) to get a better idea. 


* You can read about all other utilities in [Databricks Utilies's documentation](https://docs.databricks.com/user-guide/dev-tools/dbutils.html)