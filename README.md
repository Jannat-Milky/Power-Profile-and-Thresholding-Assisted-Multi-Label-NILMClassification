
# Reproducibility Package — Green Multi-Class NILM (Green Computing Analysis)

This repository contains the CODE and REPORT used to reproduce the experimental results reported in the paper “Green Multi-Class NILM: Green and
Energy-Efficient Multi-Class Non-Intrusive Load
Monitoring Using Data-Driven Thresholding and
Classical Machine Learning on Low-Frequency
Smart Meter Data”, including classification performance and runtime-based energy efficiency analysis.

**1. Execution Environment**

Platform: Kaggle Notebook

Hardware: CPU-only

Programming Language: Python 3.10

Operating System: Linux (Kaggle default)

Required Python Libraries

numpy

pandas

scikit-learn

matplotlib

seaborn

itertools

time

(All libraries are pre-installed in Kaggle.)

**2. Dataset Description**

Dataset name: REDD (Reference Energy Disaggregation Dataset)

Source: Kaggle
https://www.kaggle.com/datasets/joragasy/redd-dataset

House used: House 2

Sampling rate: approximately 1 Hz

Data type: Power consumption in Watts

Input files: CSV files corresponding to individual appliances in House 2

Only House 2 data are used in all experiments.

**3. Preprocessing Pipeline**

The following preprocessing steps are applied:

Load appliance-level CSV files using pandas.

Convert timestamps to datetime format.

Merge appliance data using an outer join.

Replace missing values with zero.

Clip negative power readings to zero.

Ensure all values are numeric.

Apply a minimum ON/OFF threshold of 10 W.

Compute appliance-specific power windows using the 5th–95th percentiles.

Encode appliance states as binary ON/OFF values.

Combine binary appliance states into multi-class labels.

Remove appliance combinations with fewer than 20 samples.

**4. Feature Definition**

Input feature: Aggregate power (main meter only)

Appliance-level power signals are not used as model inputs.

**5. Models and Hyperparameters**

The following classifiers are evaluated:

CART: max_depth = 10

Random Forest: n_estimators = 100, max_depth = 10

Extra Trees: n_estimators = 100, max_depth = 10

KNN: n_neighbors = 5, weights = uniform

KNN-CB: n_neighbors = 10, weights = distance

LDA: default parameters

Gaussian Naive Bayes

**6. Training and Testing Setup**

Train–test split: 80% training / 20% testing

Stratified sampling: Enabled

Random seed: 42

**7. Evaluation Metrics**

Accuracy: Overall classification accuracy.

Macro F1-score: Mean F1-score across all classes, treating each class equally.

Weighted F1-score: F1-score weighted by class frequency.

**8. Energy and Green Computing Analysis**

Direct hardware-level energy consumption (kWh) is not measured.

Energy efficiency is approximated using wall-clock runtime, measured with Python’s time module during model training and inference.

Under a fixed CPU-only Kaggle execution environment, shorter runtime is assumed to correlate with lower energy consumption. This proxy supports relative efficiency comparison across models, but does not represent absolute energy usage.

**9. SLA Violations**

SLA violations (%) are not computed in this work.

No latency or response-time constraints are defined in the experimental setup.

**10. How to Run the Code**

Open a Kaggle notebook.

Add the REDD dataset (House 2) from Kaggle:
https://www.kaggle.com/datasets/joragasy/redd-dataset

Upload nilm-ewu.ipynb from CODE.

Run the notebook or Python script sequentially.

The output metrics will be printed in the notebook.

**11. Output Mapping**

Table IV (Classification Results): Generated from printed accuracy and F1-score outputs.

Table VI (Runtime / Efficiency Results): Generated from recorded runtime measurements for each model.

**12. Notes on Reproducibility**

Results are reproducible under the same Kaggle CPU environment and random seed. Minor runtime variations may occur due to shared resource scheduling.
