# **VI Apache Spark**

#### **Q1. How would you compute the total count of unique words in Spark? Explain with appropriate example program.**

**Goal:** Count number of unique words in a text file using PySpark.

```python
from pyspark import SparkContext
sc = SparkContext()

text = sc.textFile("file.txt")
words = text.flatMap(lambda line: line.split())
unique_words = words.distinct()
count = unique_words.count()

print("Total unique words:", count)
```

**Steps:**

1. Load text file → `textFile()`
2. Split words → `flatMap()`
3. Get unique words → `distinct()`
4. Count → `count()`

---

#### **Q2. Elaborate in detail about Spark architecture with appropriate diagrams.**

**Core Components:**

1. **Driver Program** – Runs main function & schedules jobs.
2. **Cluster Manager** – YARN / Mesos / Standalone.
3. **Executors** – Run tasks and store data.
4. **RDD** – Resilient Distributed Dataset.

**Diagram Tip (sketch idea):**

```
Driver Program
   |
   |-- Tasks → Cluster Manager → Executors
```

**Key Concepts:**

* **Lazy Evaluation**
* **In-memory computation**
* **Fault tolerance using DAG and lineage**

---

#### **Q3. Explain in detail about the steps for building Spark ML pipeline.**

**Steps to Build ML Pipeline:**

1. **Load Data**
2. **Data Cleaning**
3. **Feature Extraction** – Use `VectorAssembler`, `StringIndexer`
4. **Model Training** – E.g., `LogisticRegression()`
5. **Pipeline Creation**
6. **Fit & Transform**
7. **Evaluate**

**Example Code:**

```python
from pyspark.ml import Pipeline
from pyspark.ml.feature import VectorAssembler
from pyspark.ml.classification import LogisticRegression

assembler = VectorAssembler(inputCols=["feature1", "feature2"], outputCol="features")
lr = LogisticRegression(featuresCol="features", labelCol="label")

pipeline = Pipeline(stages=[assembler, lr])
model = pipeline.fit(training_data)
```

---

#### **Q4. List out the types of Spark ML algorithms and explain in detail about logistic regression used for prediction in Spark environment.**

**Types of Spark ML Algorithms:**

1. **Classification** – Logistic Regression, Decision Tree
2. **Regression** – Linear Regression
3. **Clustering** – KMeans
4. **Recommendation** – ALS
5. **Dimensionality Reduction** – PCA

**Logistic Regression in Spark:**

* Used for **binary classification** (e.g., spam vs. not spam).
* Computes probability using **sigmoid** function.
* Example:

```python
from pyspark.ml.classification import LogisticRegression
lr = LogisticRegression(featuresCol="features", labelCol="label")
model = lr.fit(train_data)
```

---

#### **Q5. Explain in detail about the model inference, deployment, and export a deployed model in Spark environment.**

**Model Inference:**

* Use `.transform(test_data)` to get predictions.

**Deployment Steps:**

1. **Train model using pipeline**
2. **Save model:**

```python
model.write().overwrite().save("model_path")
```

3. **Load model:**

```python
from pyspark.ml.pipeline import PipelineModel
model = PipelineModel.load("model_path")
```

**Use Cases:**

* Deployed in streaming apps (Spark Streaming)
* Exported for APIs or batch jobs

---

#### **Q6. Explain in detail about hyperparameter training and AutoML in PySpark.**

**Hyperparameter Tuning:**

* Use **CrossValidator** or **TrainValidationSplit** with parameter grid.

```python
from pyspark.ml.tuning import ParamGridBuilder, CrossValidator
grid = ParamGridBuilder().addGrid(lr.regParam, [0.1, 0.01]).build()
cv = CrossValidator(estimator=pipeline, estimatorParamMaps=grid, evaluator=evaluator, numFolds=3)
best_model = cv.fit(training_data)
```

**AutoML in PySpark:**

* PySpark does **not natively support AutoML**, but tools like:

  * **MLflow + HPO**
  * **Databricks AutoML**
  * **Hyperopt + SparkTrials**
    can enable AutoML pipelines.
