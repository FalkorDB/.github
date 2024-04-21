[![Try Free](https://img.shields.io/badge/Try%20Free-FalkorDB%20Cloud-FF8101?labelColor=FDE900&style=for-the-badge&link=https://app.falkordb.cloud)](https://app.falkordb.cloud)

**Our objective is to create an outstanding Knowledge Graph specifically for Large Language Models (LLM) that boasts exceptionally low latency, ensuring swift delivery of information through our Graph Database, known as KG-RAG.**

FalkorBD is the first queryable [Property Graph](https://github.com/opencypher/openCypher/blob/master/docs/property-graph-model.adoc) database to use [sparse matrices](https://en.wikipedia.org/wiki/Sparse_matrix) to represent the [adjacency matrix](https://en.wikipedia.org/wiki/Adjacency_matrix) in graphs and [linear algebra](http://faculty.cse.tamu.edu/davis/GraphBLAS.html) to query the graph.

Primary features:
* Adopting the [Property Graph Model](https://github.com/opencypher/openCypher/blob/master/docs/property-graph-model.adoc)
  * Nodes (vertices) and Relationships (edges) that may have attributes
  * Nodes can have multiple labels
  * Relationships have a relationship type
* Graphs represented as sparse adjacency matrices
* [OpenCypher](http://www.opencypher.org/) with proprietary extensions as a query language
  * Queries are translated into linear algebra expressions
