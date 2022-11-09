# vector-similarity-w-vertex-ai
end-to-end visual similarity solution using Vertex Matching Engine

- [insert_notebook_link_here] instructions for downloading and preparing the [Retail Product Dataset](https://www.kaggle.com/c/retail-products-classification/data)

![alt text](https://github.com/tottenjordan/vector-similarity-w-vertex-ai/blob/main/imgs/visual-sim-ref-arch.png)

### Neural Deep Retrieval

1. Use a pretrained deep learning model to extract feature vectors (embeddings) from each image in a retail product catalog

2. Store embedding vectors in a scalable approximate nearest neighbor (ANN) index, e.g., [Vertex Matching Engine](https://cloud.google.com/vertex-ai/docs/matching-engine/overview), where each image's embedding vectors are indexed by product ID

3. For a given query image, call `model.predict(x)` with the same pretrained model used in (1) to extract the feature vectors (embeddings) from the query image

4. Using the computed feature vectors from (3), query the Matching Engine Index to find the `k` nearest neighbors

#### TODOs: 
* (1) add upload/deploy pre-trained model to Vertex Registry/Prediction, 
* (2) pre-built components for steps in (1), 
* (3) deploy ANN & Brute Force indices to different endpoints
