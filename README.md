# WiFi-Indoor-Localization-Using-Machine-Learning
This project implements a WiFi-based indoor localization system using classical machine learning techniques. Using Received Signal Strength Indicator (RSSI) fingerprints from the UJIIndoorLoc dataset, the system predicts:

- Building ID (classification)
- Floor level (classification)
- Longitude and Latitude coordinates (regression)

The goal is to evaluate how well traditional machine learning models can perform indoor localization in high-dimensional and noisy environments.

# Dataset Overview
This project uses the UJIIndoorLoc dataset, a large-scale multi-building, multi-floor indoor localization benchmark.

Dataset characteristics:
- ~19,000 training samples
- 520 WiFi Access Point (WAP) RSSI features
- Labels: Building ID, Floor, Longitude, Latitude
- RSSI values range from –104 dBm to 100
- A value of 100 indicates no signal detected

The dataset is not included in this repository due to its large size. 

# Dataset Download instructions:

- Dataset: https://archive.ics.uci.edu/ml/datasets/ujiindoorloc
- Download trainingData.csv and validationData.csv
- Place them in the project root or /data directory

# Methodology

The project follows a structured machine learning pipeline designed to address the challenges of high-dimensional and sparse WiFi RSSI data. All models were trained on the preprocessed training set and evaluated on a held-out validation set. Cross-validation was additionally used to assess model stability and generalization:

1. Preprocessing

- RSSI values of 100 (no signal detected) are replaced with -105 dBm to represent extremely weak but physically plausible signals
- Features are standardized using StandardScaler
- Low-variance WAP features are removed using a variance threshold filter
- Dimensionality reduction is applied using Principal Component Analysis (PCA)

2. Dimensionality Reduction

- Multiple PCA configurations were tested
- 200 principal components were selected, preserving ~90–95% of total variance
- PCA reduces noise, mitigates sparsity, and improves model generalization

3. Models Evaluated
   
- Classification (BuildingID & Floor):
  
    - K-Nearest Neighbors (KNN)
    - Random Forest
    - XGBoost

- Regression (Longitude, Latitude, & Floor):

  - K-Nearest Neighbors Regressor
  - Random Forest Regressor
  - XGBoost Regressor (multi-output)

# Evaluation Metrics

- Accuracy for building and floor classification
- Mean Absolute Error (MAE) for regression tasks (longitude, latitude, floor)
- Confusion Matrices

# Results Summary
Classification Performance:

- Building classification: up to 100% accuracy
- Floor classification: approximately 82%–88% accuracy

Regression Performance (MAE):

- Longitude MAE: 6.46–7.45
- Latitude MAE: 5.91–7.35
- Floor MAE: 0.22–0.36

# Key Takeaways

- WiFi RSSI fingerprints contain highly discriminative spatial information
- Classical machine learning models remain competitive for indoor localization
- PCA is critical for handling high-dimensional, sparse RSSI features
- Tree-based ensemble models perform robustly under signal noise and variability
- Strong results can still be achieved without deep learning methods
