# Customer Churn Prediction with Spark ML on Amazon EMR

## Dataset
**Bank Customer Churn Dataset** from Kaggle:  
[https://www.kaggle.com/datasets/shrutimechlearn/churn-modelling](https://www.kaggle.com/datasets/shrutimechlearn/churn-modelling)  

**Description:**  
The dataset contains information about bank customers, including:

- `CreditScore` — Customer credit score  
- `Geography` — Country (France, Spain, Germany)  
- `Gender` — Male or Female  
- `Age` — Customer age  
- `Tenure` — Number of years the customer has been with the bank  
- `Balance` — Account balance  
- `NumOfProducts` — Number of bank products used  
- `EstimatedSalary` — Estimated salary of the customer  
- `Exited` — Target variable: 0 = customer stayed, 1 = customer churned  

The dataset is used to train a machine learning model to predict customer churn.

---

## Running the Spark ML Pipeline

### 1. Upload dataset to EMR Master Node
```bash
scp -i vockey.pem Churn_Modelling.csv hadoop@<master-public-dns>:/home/hadoop/
```

2. Copy dataset to HDFS
hdfs dfs -mkdir -p /user/hadoop/churn_input
hdfs dfs -put Churn_Modelling.csv /user/hadoop/churn_input/
3. Run the Spark job
spark-submit --master yarn --deploy-mode client churn_pipeline.py

The pipeline performs the following steps:
Load data from HDFS
Encode categorical features (Geography, Gender)
Assemble features into a vector
Scale features
Train Logistic Regression model
Make predictions
Evaluate accuracy
4. Notes
Accuracy will be printed at the end of the job, e.g.:
Accuracy: 0.7929
Feature ablation experiments can be performed by removing categorical features and rerunning the pipeline.
