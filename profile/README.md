[![Try Free](https://img.shields.io/badge/Try%20Free-FalkorDB%20Cloud-FF8101?labelColor=FDE900&link=https://app.falkordb.cloud)](https://app.falkordb.cloud)
[![Discord](https://img.shields.io/discord/1146782921294884966?style=flat-square)](https://discord.gg/6M4QwDXn2w)

**Our objective is to create an outstanding Knowledge Graph specifically for Large Language Models (LLM) that boasts exceptionally low latency, ensuring swift delivery of information through our Graph Database, known as GraphRAG.**

FalkorBD is the first queryable [Property Graph](https://github.com/opencypher/openCypher/blob/master/docs/property-graph-model.adoc) database to use [sparse matrices](https://en.wikipedia.org/wiki/Sparse_matrix) to represent the [adjacency matrix](https://en.wikipedia.org/wiki/Adjacency_matrix) in graphs and [linear algebra](http://faculty.cse.tamu.edu/davis/GraphBLAS.html) to query the graph.

Primary features:
* Adopting the [Property Graph Model](https://github.com/opencypher/openCypher/blob/master/docs/property-graph-model.adoc)
  * Nodes (vertices) and Relationships (edges) that may have attributes
  * Nodes can have multiple labels
  * Relationships have a relationship type
* Graphs represented as sparse adjacency matrices
* [OpenCypher](http://www.opencypher.org/) with proprietary extensions as a query language
  * Queries are translated into linear algebra expressions


## What you can build with FalkorDB

* **[GraphRAG](https://www.falkordb.com/graphrag/)** &mdash; Combine knowledge graphs with retrieval-augmented generation to give LLMs accurate, low-latency context. Get started with the [GraphRAG-SDK](https://github.com/FalkorDB/GraphRAG-SDK).
* **[Code-Graph](https://github.com/FalkorDB/code-graph)** &mdash; Explore, analyze and visualize your codebase as a knowledge graph to power code understanding and AI assistants.
* **Agentic Memory** &mdash; Use FalkorDB as the graph-backed memory layer for AI agents through popular frameworks:
  * [Mem0](https://github.com/mem0ai/mem0)
  * [Cognee](https://github.com/topoteretes/cognee)
  * [Graphiti](https://github.com/getzep/graphiti)
* **[QueryWeaver](https://github.com/FalkorDB/QueryWeaver)** &mdash; An open-source Text2SQL tool that turns natural language into SQL using graph-powered schema understanding, letting you ask your database questions in plain English.
