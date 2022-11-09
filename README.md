# vector-similarity-w-vertex-ai
end-to-end visual similarity solution using Vertex Matching Engine

- [01-prepare-vpc-network.ipynb](https://github.com/tottenjordan/vector-similarity-w-vertex-ai/blob/main/01-prepare-vpc-network.ipynb) - steps for creating the required VPC network config
- [02-retail-dataset-prep.ipynb](https://github.com/tottenjordan/vector-similarity-w-vertex-ai/blob/main/02-retail-dataset-prep.ipynb) instructions for downloading and preparing the [Retail Product Dataset](https://www.kaggle.com/c/retail-products-classification/data)
- [03-pipeline-workflows.ipynb](https://github.com/tottenjordan/vector-similarity-w-vertex-ai/blob/main/03-pipeline-workflows.ipynb) - orchestrate e2e workflow with Vertex Pipelines
- [04-vector-filtering.ipynb](https://github.com/tottenjordan/vector-similarity-w-vertex-ai/blob/main/04-vector-filtering.ipynb) - examples of filtering and crowding when querying index

### TODOs: 
* (1) Use both image and text (product title, description) for embeddings

reference architecture
![alt text](https://github.com/tottenjordan/vector-similarity-w-vertex-ai/blob/main/imgs/visual-sim-ref-arch.png)

### Objectives

1. Use a pretrained deep learning model to extract feature vectors (embeddings) from each image in a retail product catalog

2. Store embedding vectors in a scalable approximate nearest neighbor (ANN) index, e.g., [Vertex Matching Engine](https://cloud.google.com/vertex-ai/docs/matching-engine/overview), where each image's embedding vectors are indexed by product ID

3. For a given query image, call `model.predict(x)` with the same pretrained model used in (1) to extract the feature vectors (embeddings) from the query image

4. Using the computed feature vectors from (3), query the Matching Engine Index to find the `k` nearest neighbors

### Vertex Pipelines
![alt text](https://github.com/tottenjordan/vector-similarity-w-vertex-ai/blob/main/imgs/vsm-e2e-pipe.png)

* **Load / pre-process images**
> * decode
> * reshape per model specs
> * Convert tensor to float & add axis for expected model input (e.g., `1 x 224 x 224 x 3`)

* **Extract Feature Vectors**
> * Load pre-trained image model ([TF Hub](https://tfhub.dev/))
> * Loop through images & calculate feature vectors (embeddings)
> * Save vectors to file in Cloud Storage

* **Build Matching Engine Index**
> * [Setup VPC Network Peering Connection](https://cloud.google.com/vertex-ai/docs/matching-engine/using-matching-engine#vpc-network-peering-setup)
> * [NearestNeighborSearchConfig](https://cloud.google.com/vertex-ai/docs/matching-engine/configuring-indexes#nearest-neighbor-search-config) e.g., `dimensions`, `approximateNeighborsCount`, `distanceMeasureType`, etc.


### Feature Extraction

* Pre-trained models trained on larger datasets can be a good starting point.
* If the original dataset is large and general enough, the spatial hierarchy of features learned by the pretrained network can effictevly act as a generic modelof the vidual world
* They can be useful even if the image classes are completely different between the original and target dataset  
* **Feature Extraction** consists of taking the convolutional base of a previously trained network, running new data through it, and training a new classifier on top of the output
