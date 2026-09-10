# PageRank Analysis of Wikipedia with PySpark

Implementation of the **PageRank algorithm** using **PySpark DataFrames** and **Databricks** to estimate the importance of Wikipedia articles based on the structure of links between them.

This project was developed as part of a university project at **Universidad Carlos III de Madrid (UC3M)**, focusing on distributed data processing and graph-based algorithms.

---

##  Project Overview

PageRank is an algorithm originally developed for ranking web pages according to the importance of their incoming links.

In this project, PageRank is applied to a large-scale dataset of Wikipedia articles. The main challenge is to process the graph efficiently using **distributed computation with Apache Spark**, avoiding unnecessary data transfers to the driver.

The implementation builds the link structure between Wikipedia articles and iteratively computes their PageRank scores until convergence.

---

##  Dataset

The project uses the public English Wikipedia dataset available in **Databricks**.

* **Source:** Databricks public Wikipedia dataset
* **Format:** Apache Parquet
* **Path:**
  `dbfs:/databricks-datasets/wikipedia-datasets/data-001/en_wikipedia/articles-only-parquet`
* **Sampling:** 10% of the dataset was used during development to reduce computational requirements.

The original dataset is **not included in this repository** because of its large size. It is accessed directly from the Databricks environment.

---

##  Technologies

* **Python**
* **PySpark**
* **Apache Spark**
* **Databricks**
* **Apache Parquet**
* **Pandas**
* **Regular Expressions**

The implementation relies primarily on Spark DataFrames and native Spark functions for distributed processing.

---

##  Methodology

### 1. Data Loading

Wikipedia articles are loaded from the Databricks filesystem using the Parquet format.

### 2. Link Extraction

Outgoing links are extracted from the text of each Wikipedia article.

### 3. ID Mapping

Wikipedia page titles are converted into numerical identifiers to reduce memory usage and make subsequent graph operations more efficient.

### 4. Graph Construction

The Wikipedia link structure is represented using two main relationships:

* **Forward links:** pages linked by each article.
* **Reverse links:** pages that link to a given article.

This representation allows the PageRank score to be propagated efficiently through the graph.

### 5. Iterative PageRank Computation

Each page is initially assigned an equal PageRank score.

The score is then iteratively updated according to the PageRank formulation, using a damping factor and accounting for pages without outgoing links.

### 6. Convergence

The algorithm stops when the difference between consecutive iterations becomes sufficiently small or when the maximum number of iterations is reached.

---

## Distributed Computing & Optimization

A major focus of the project was implementing the algorithm efficiently in a distributed environment.

### Spark-native operations

Native PySpark functions were preferred over unnecessary Python UDFs. For example, Spark functions such as `size()` were used to perform operations directly on the cluster.

### Distributed computation

The computationally intensive operations — including joins, aggregations and PageRank propagation — are performed using Spark DataFrames across the cluster.

Only small aggregated results are transferred to the driver when required, such as when checking convergence.

### Memory efficiency

Page titles are mapped to numerical IDs, reducing the amount of data that needs to be processed during the iterative computation.

---

##  Results

The implementation successfully computes PageRank scores for the Wikipedia graph and identifies the articles with the highest authority according to their link structure.

The resulting ranking reflects the connectivity of Wikipedia articles while maintaining a distributed processing workflow.

---

##  Key Takeaways

This project provided practical experience with:

* Distributed data processing with **Apache Spark**
* **PySpark DataFrames**
* Graph representation and iterative algorithms
* Large-scale data processing
* Databricks
* Apache Parquet
* Spark memory and performance considerations
* Convergence-based iterative computation

---

##  How to Run

The notebook was developed for **Databricks**, as the dataset is accessed directly through the Databricks filesystem.

1. Open a Databricks workspace.
2. Import the notebook included in this repository.
3. Attach the notebook to a Spark cluster.
4. Run the cells sequentially.

The required dataset is available at:

```text
dbfs:/databricks-datasets/wikipedia-datasets/data-001/en_wikipedia/articles-only-parquet
```

---

##  Project

University project developed at **Universidad Carlos III de Madrid (UC3M)**.

**Author:** Ainhoa Santano and Marta Gómez
