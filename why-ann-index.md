# Efficient retrieval for real time serving
Why do we need an ANN index for efficient, real time serving in retrieval and similarity search use cases?

### 1) Given a query, we search a corpus of items for the most relevant candidate item(s)

In retrieval, we have query items (such as an image), and the goal is to query a large database, in such a way that the query results return items that are more similar to the query than any other items in the database

![alt text](https://github.com/tottenjordan/vector-similarity-w-vertex-ai/blob/main/imgs/i-use-case.png)

### 2) Exhaustive search == infeasible at scale

One approach is to calculate the similarity between the `query_item` and all items in the database, i.e., an *exhaustive search (brute force)*

... but this quickly becomes infeasible with large datasets

![alt text](https://github.com/tottenjordan/vector-similarity-w-vertex-ai/blob/main/imgs/i-brute-force.png)

### 3) Approximate search == efficient at scale

A critical component for an *approximate search* is an index-structure optimized for efficient retrieval
* divides dataset into subsets
* limit search to subset of candidate items (sub-linear)

![alt text](https://github.com/tottenjordan/vector-similarity-w-vertex-ai/blob/main/imgs/i-ann-retireve.png)

### 4) Neural Deep Retrieval (NDR) --> Vertex Matching Engine

NDR provides a way for us to represent complex relationships between multiple entities, [Vertex Matching Engine](https://cloud.google.com/vertex-ai/docs/matching-engine/overview) is a managed solution for indexing these entities
* use deep learning model (encoder) to generate embedding vector representations of all items
* with embedding vectors, build a serving index that orients similar items closer to each other

![alt text](https://github.com/tottenjordan/vector-similarity-w-vertex-ai/blob/main/imgs/high-level-NDR.png)

