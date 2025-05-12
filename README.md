# Security-Log-Anomaly-Detection-System
Build a system that collects simulated security logs and detects anomalies in real time using statistical and ML techniques.

To develop a real-time anomaly detection system that identifies and visualizes suspicious network activity by simulating log streams from the UNSW-NB15 dataset. 

## Dataset

I have used [UNSW-NB15 dataset](https://research.unsw.edu.au/projects/unsw-nb15-dataset), which is a network intrusion dataset. It contains nine different attacks, includes DoS, worms, Backdoors, and Fuzzers. I have specifically utilised [UNSW-NB15_1.csv](https://drive.google.com/file/d/1Xs8676kjZX8y5oVjiCplZL5zdQPTfk0j/view?usp=sharing) containing key network-level attributes and a `label` column for ground truth.


## Project Objectives

1.  Detect anomalous activity in network logs using an unsupervised model.
2.  Visualize and explore trends, patterns, and predictions in Tableau.

## Methodology

I have built this project in 3 seperate code files. 

**1. Data Preprocessing (preprocessing.ipynb)**

*  Handled missing values and inconsistent types. Created a clean version of the dataset ready for modeling.
*  Created a clean label column by replacing missing label values (NaN) with randomly assigned 0 (normal) or 1 (anomaly), since ground truth labels were missing.
*  Added a synthetic log_id column to uniquely identify and sequence logs for visualization purposes.

**2. Simulating Real-Time Streaming (log_streamer.ipynb)**

* It Reads logs from the cleaned prediction file row-by-row, simulating incoming network events.
* It streams entries in a structured JSON log format.

**3. Anomaly Detection Using Isolation Forest (anomaly_detection.ipynb)**

* The anomaly detection task was framed as an unsupervised outlier detection problem using the Isolation Forest algorithm, well-suited for high-dimensional and large-scale log data.
* Split the cleaned dataset into training (80%) and testing (20%) sets. Trained an Isolation Forest model (n_estimators=100, contamination=0.1) using only the training data.
* Predicted anomaly scores on the test set.
      * Model output of -1 was interpreted as an anomaly and mapped to label 1
  
      * Output of 1 was mapped to normal, label 0.

## Results & Analysis
The anomaly detection model was evaluated on a test set of 140,001 network log entries using synthetic labels (0 = normal, 1 = anomaly). 

1. Overall training and testing accuracy are 82.04% and 81.87% respectively.

| Metric | Normal (0) | Anomaly(1) |
| ------------- | ------------- | ------------- |
| Precision  | 0.90  |      0.09        |
| Recall  | 0.90  |        0.09       |
|F1 Score|    0.90                |      0.09         |
|Support|         126,021 |	13,980     |

2. Confusion Metrix :

<img width="497" alt="Screenshot 2025-05-12 at 2 50 21 PM" src="https://github.com/user-attachments/assets/1c496bec-ee54-4a83-94a8-9ba85ec4f053" />


  
