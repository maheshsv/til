# Apache Parquet

> Apache Parquet is a columnar storage format available to any project in the Hadoop ecosystem, regardless of the choice of data processing framework, data model or programming language.

## Read/Write Parquet File

### Read/Write with Apache Spark and Scala (on MacOS)

Using Apache Spark to write to and read from Parquet file is the easiest way I found.

Prerequisites:

- Install Scala with Homebrew: `brew install scala`.
- Install Spark with Homebrew:  `brew install apache-spark`.
- Install Parquet-tools, it's a handy command line tool to read Parquet file: `brew install parquet-tools`.

To read from/write to Parquet file with Spark. Run `spark-shell` to open a Spark session:

```scala
case class Person(name: String, age: Integer)
val data = Seq(Person("Alice", 4), Person("Bob", 20), Person("John", 100))
val df = data.toDF()

// Write to file in Parquet format
df.write.parquet("/tmp/parquet-test")

// Read from Parquet files
val sqlContext = new org.apache.spark.sql.SQLContext(sc)
val dfPeople = sqlContext.read.parquet("/tmp/parquet-test")
val people = dfPeople.as[Person].collect()
people(0)
people(1)
people(2)
```

Go to the file path and check the Paquet files there. You can use parquet-tools to read the files as well:

```bash
parquet-tools cat <fileName>
```

I also created this small [ParquetDemo](https://github.com/guihaojin/ParquetDemo) project to show how to serialize Java objects to Parquet format and read back form Parquet file to Java objects.
