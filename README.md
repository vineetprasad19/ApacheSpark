# ApacheSpark
Apache Spark is an open source parallel processing framework for running large-scale data analytics apps across clustered computers. It can handle both real and batch jobs and data processing workloads.

1. Spark follows lazy evaluation technique and not like (Map Reduce Linear evaluation)  
2. Bottom to top approach (action to rdd) and not like (Map Reduce where it does top to bottom approch)  
3. Uses in-memory processing so not hitting your hard disk frequently.  

# Key Features of Apache Spark:  
**Speed:**  
Spark can process data up to 100 times faster than traditional big data frameworks like Hadoop MapReduce.  
Utilizes in-memory computing and optimized execution plans.  
**Ease of Use:**  
Provides APIs in multiple languages, including Scala, Python, Java, R, and SQL.  
Supports interactive queries and shell-based processing.  
**Unified Engine:**  
A single framework for various workloads, such as:  
Batch processing: Process large-scale data sets.  
Stream processing: Handle real-time data streams (e.g., Kafka).   
Machine learning: Built-in library called MLlib.  
Graph processing: Library for graph algorithms called GraphX.  
**Distributed Computing:**  
Runs computations across a cluster of machines.  
Automatically handles fault tolerance and data replication.  
**Integration:**  
Works seamlessly with big data tools and storage systems like Hadoop HDFS, Apache Kafka, Cassandra, and AWS S3.  
Provides support for structured data processing using Spark SQL.  

# Components of Apache Spark:  
**Core:**  
The foundation of Spark that provides basic functionalities like task scheduling, memory management, and fault recovery.  
Supports resilient distributed datasets (RDDs) for fault-tolerant, distributed data processing. **RDD** is an immutable collection of objects. It is read only, partition collection of records. RDD basically represents the data across nodes in the cluster
**Operations of RDD:** **Transformations** (for filter the data) and **Actions** (Gives final outputs)  
**Spark SQL:**  
Provides support for structured data processing using SQL-like queries.  
Can read data from various sources (e.g., Hive, Parquet, JSON, CSV).  
**Spark Streaming:**  
Processes real-time streaming data.  
Suitable for applications like log processing and real-time dashboards.  
**MLlib:**  
A scalable machine learning library that includes algorithms for classification, regression, clustering, and recommendation.  
**GraphX:**  
A library for graph processing and analysis.  
Supports graph algorithms like PageRank and connected components.  
**Structured Streaming:**  
A modern API for stream processing that integrates with Spark SQL.  

# Use Cases of Apache Spark:   
**Big Data Analytics:** Processing large-scale data in industries like e-commerce, healthcare, and finance.   
**Real-Time Data Processing:** Monitoring streams of data from IoT devices, log files, or social media.   
**Machine Learning:** Building recommendation systems, predictive models, and clustering.  
**ETL (Extract, Transform, Load):** Data ingestion and transformation workflows.  
**Graph Processing:** Social network analysis and recommendation graphs.  

# Why Use Apache Spark?  
**In-Memory Computing:** Faster processing by keeping data in memory during computations.  
**Flexibility:** Multi-language support and wide-ranging applications.  
**Scalability:** Can process petabytes of data across large clusters.  
**Community Support:** A large, active community ensures continuous improvements and robust documentation.  

**Apache Spark is a cornerstone of modern big data processing and is widely used across industries for handling large-scale and complex data workflows.**  

# 1. Setup and Initialization  
Python (PySpark):    
from pyspark.sql import SparkSession    
**Create a Spark Session**  
spark = SparkSession.builder \  
    .appName("BasicSparkExample") \  
    .getOrCreate()    
print("Spark Session Initialized")  

Scala:    
import org.apache.spark.sql.SparkSession  

// Create a Spark Session  
val spark = SparkSession.builder()  
    .appName("BasicSparkExample")  
    .getOrCreate()  
  
println("Spark Session Initialized")  
# 2. Loading and Viewing Data  
Python (PySpark):  
**Load a CSV file into a DataFrame**  
df = spark.read.csv("example.csv", header=True, inferSchema=True)  

**Show the first few rows**  
df.show()  

Scala:    
// Load a CSV file into a DataFrame  
val df = spark.read  
    .option("header", "true")  
    .option("inferSchema", "true")  
    .csv("example.csv")    
// Show the first few rows  
df.show()  
# 3. Basic Transformations and Actions  
Python (PySpark):    
//Filter rows where a column value is greater than a threshold//    
filtered_df = df.filter(df["column_name"] > 50)    
//Select specific columns  
selected_df = filtered_df.select("column_name", "another_column")  
//Show results  
selected_df.show()    
//Count rows  
row_count = selected_df.count()  
print(f"Row count: {row_count}")  

Scala:   
// Filter rows where a column value is greater than a threshold  
val filteredDf = df.filter($"column_name" > 50)    
// Select specific columns  
val selectedDf = filteredDf.select("column_name", "another_column")    
// Show results  
selectedDf.show()    
// Count rows  
val rowCount = selectedDf.count()  
println(s"Row count: $rowCount")  

# 4. Spark SQL Example  
Python (PySpark):    
//Register a DataFrame as a temporary SQL table  
df.createOrReplaceTempView("example_table")    
//Use SQL to query the table  
result = spark.sql("SELECT column_name, COUNT(*) as count FROM example_table GROUP BY column_name")  
//Show the result  
result.show()  
  
Scala:  
// Register a DataFrame as a temporary SQL table  
df.createOrReplaceTempView("example_table")    
// Use SQL to query the table  
val result = spark.sql("SELECT column_name, COUNT(*) as count FROM example_table GROUP BY column_name")    
// Show the result  
result.show()   

# 5. Write Data to Storage  
Python (PySpark):    
//Write DataFrame to a Parquet file
df.write.parquet("output_path")  

Scala:    
// Write DataFrame to a Parquet file  
df.write.parquet("output_path")  

# 6. Streaming Example  
Python (PySpark):  
//Read streaming data from a directory  
stream_df = spark.readStream \  
    .format("csv") \  
    .option("header", "true") \  
    .schema(df.schema) \  
    .load("streaming_data_path") 
//Write streaming data to the console  
query = stream_df.writeStream \  
    .outputMode("append") \  
    .format("console") \  
    .start()    
query.awaitTermination()  
  
Scala:    
// Read streaming data from a directory  
val streamDf = spark.readStream  
    .format("csv")  
    .option("header", "true")  
    .schema(df.schema)  
    .load("streaming_data_path")    
// Write streaming data to the console  
val query = streamDf.writeStream  
    .outputMode("append")  
    .format("console")  
    .start()  
query.awaitTermination()  
   
**These above examples shows how to perform basic operations with Spark, including creating a session, loading data, transforming datasets, querying with SQL, writing data to storage, and processing streaming data.**  
