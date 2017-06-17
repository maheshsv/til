# BigQuery

### What is BigQuery

BigQuery is a query service for very large dataset at blazing fast speed provided by Google. It's a public implementation of Dremel that was one of the core technologies at Google.

### Why it's so fast

- Columnar Storage: data is stored in columnar storage fashion.
- Tree Architecture: use tree structure to dispatch queries and aggregate results.

[Here](https://cloud.google.com/files/BigQueryTechnicalWP.pdf) you can find more about the technical details, common use cases and comparison with MapReduce.

[^footnote]: [Dremel paper](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/36632.pdf)
