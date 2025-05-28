# Home_Sales Analysis with PySpark

In this challenge, we are analyzing home sales data using PySpark and SparkSQL. The goal is to derive key metrics from the dataset, perform various SQL queries, and optimize performance through cacheing and partitioning.
We are provided with home_sales_revised.csv dataset, which is read from an AWS S3 bucket.

We have to include the code **!pip install findspark** to install the 'findspark' library to use the python API for spark.

* Create a temporary view of the DataFrame
  
  df.createOrReplaceTempView("home_sales")
  
* Cache the the temporary table home_sales.
  
  spark.sql("cache table home_sales")
  
* Check if the table is cached.
  
  spark.catalog.isCached('home_sales')
  
* Partition by the "date_built" field on the formatted parquet home sales data
  
  df.write.partitionBy("date_built").parquet("home_sales_partitionby", mode = "overwrite")

* Uncache the home_sales temporary table.
  
  spark.sql("uncache table home_sales")

The runtime improved significantly from 1.21 seconds (uncached) to 0.66 seconds (cached), demonstrating the efficiency gained through caching.
Additionally, the runtime for the partitioned query was 1.47 seconds, which is not an improvement when compared to the uncached runtime. This indicates that partitioning alone did not enhance performance.
  

