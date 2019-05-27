Spark has three data representations viz RDD, Dataframe, Dataset. 

To use Apache Spark functionality, we must use one of them for data manipulation. Let’s discuss each of them briefly:

RDD: RDD (Resilient Distributed Database) is a collection of elements, that can be divided across multiple nodes in a cluster for parallel processing. It is also fault tolerant collection of elements, which means it can automatically recover from failures. RDD is immutable, we can create RDD once but can’t change it.

Dataset: It is also a distributed collection of data. A Dataset can be constructed from JVM objects and then manipulated using functional transformations (map, flatMap, filter, etc.). As I have already discussed in my previous articles, dataset API is only available in Scala and Java. It is not available in Python and R.

DataFrame: In Spark, a DataFrame is a distributed collection of data organized into named columns. It is conceptually equivalent to a table in a relational database or a data frame. It is mostly used for structured data processing. In Scala, a DataFrame is represented by a Dataset of Rows. A DataFrame can be constructed by wide range of arrays for example, existing RDDs, Hive tables, database tables.

Transformation: Transformation refers to the operation applied on a RDD to create new RDD.

Action: Actions refer to an operation which also apply on RDD that perform computation and send the result back to driver.

Broadcast: We can use the Broadcast variable to save the copy of data across all node.

Accumulator: In Accumulator, variables are used for aggregating the information