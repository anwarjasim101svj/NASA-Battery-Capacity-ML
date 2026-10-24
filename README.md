# NASA-Battery-Capacity-ML
Battery capacity degradation analysis and machine learning using the NASA B0005 dataset.
This project analyzes the NASA B0005 lithium-ion battery dataset to investigate discharge-capacity degradation, calculate capacity-based State of Health (SOH), explore discharge-feature relationships, and evaluate machine-learning approaches for capacity estimation.

Dataset

This project currently focuses exclusively on one battery: B0005, from the NASA Prognostics Center of Excellence (PCoE) lithium-ion battery aging dataset.

Dataset download: https://phm-datasets.s3.amazonaws.com/NASA/5.+Battery+Data+Set.zip

 The raw .mat file is not included in this repository; download it from above link(Official site) and follow the applicable dataset terms.

Project Objectives
Extract and analyze battery discharge-cycle data.
Calculate capacity-based SOH relative to the first recorded discharge.
Engineer voltage, current, temperature, and discharge-duration features.
Investigate relationships between discharge features and measured capacity.
Compare Linear Regression and Random Forest models.
Evaluate lagged Linear Regression against a persistence baseline for rolling one-step-ahead capacity estimation.
Key Analysis
Extracted and analyzed 168 discharge records from B0005.
Visualized discharge capacity and capacity-based SOH over successive discharge cycles.
Explored correlations between discharge features and measured capacity.
Evaluated trend-based and retrospective capacity-estimation models.
Compared rolling one-step-ahead predictions with a persistence baseline.
Results and Visualizations
1. Battery Capacity Degradation
<img width="3566" height="1765" alt="capacity_degradation" src="https://github.com/user-attachments/assets/82a8f4e2-67de-4c16-89aa-5f502a8731e6" />




This plot shows measured discharge capacity across successive discharge records.

2. Capacity-Based State of Health
<img width="3566" height="1765" alt="capacity_soh" src="https://github.com/user-attachments/assets/eaf8ae57-9995-4c22-be25-9e9920901de8" />




SOH is calculated relative to the first recorded discharge capacity.

3. Actual vs. Predicted Capacity
<img width="3570" height="1765" alt="actual_vs_predicted" src="https://github.com/user-attachments/assets/cb033961-fbb0-46bc-a15d-201614c72a0f" />




This plot compares measured capacity with model predictions for the rolling one-step-ahead test set.

4. Feature Correlation
<img width="2968" height="1765" alt="feature_correlation" src="https://github.com/user-attachments/assets/271c2e8e-e238-4c6a-9db3-8672702f01ad" />




This plot explores relationships between discharge capacity and features such as voltage, current, temperature, and discharge duration.



Tools and Libraries
Python
NumPy
Pandas
SciPy
Matplotlib
scikit-learn
Jupyter Notebook
Visual Studio Code
How to Run
Download the NASA dataset using the link provided in the Dataset section.
Extract the dataset and place B0005.mat in the same folder as the notebook.

Install the required libraries:

pip install numpy pandas scipy matplotlib scikit-learn jupyter
Open NASA_B0005_Battery_Capacity_Project.ipynb in Jupyter Notebook or VS Code.
Restart the kernel and run all cells.

The notebook generates processed CSV files and model-comparison metrics in a local results/ directory.

State of Health Calculation

Capacity-based State of Health is calculated using:

SOH(%) = [{Qm}/{Qr}] x 100 ,
Qm - measured discharge capacity at the current cycle (Ah).
Qr - reference capacity, often the initial measured capacity or rated capacity (Ah).

In this project, the reference capacity is the first recorded discharge capacity of B0005, approximately 1.8565 Ah.

The final recorded discharge capacity is approximately 1.3251 Ah, corresponding to a capacity-based SOH of approximately 71.38% relative to the first recorded discharge.

This reference is the first measured capacity, not necessarily the manufacturer's rated capacity.

Model Evaluation

The project evaluates multiple approaches, including:

Linear Regression using discharge number.
Random Forest Regression using discharge number.
Retrospective capacity estimation using discharge-cycle features.
Lagged Linear Regression for rolling one-step-ahead estimation.
A persistence baseline that predicts the next capacity using the previous measured capacity.

The models are evaluated using Mean Absolute Error (MAE), Root Mean Squared Error (RMSE), and the coefficient of determination ((R^2)) where appropriate.

Limitations
The current analysis covers only the NASA B0005 battery dataset.
The retrospective feature model uses measurements from a completed discharge and is not a forecast made before that discharge begins.
The rolling one-step-ahead evaluation uses previously measured capacities for successive predictions; it is not a single multi-step forecast of the entire test period.
Model performance is compared with a persistence baseline. A small improvement in one metric does not establish that a model is clearly superior.
Small capacity increases between adjacent records should not automatically be interpreted as physical battery recovery.
Generalization to other battery cells, chemistries, or operating conditions has not been evaluated.
Repository Structure
NASA-Battery-Capacity-ML/
├── NASA_B0005_Battery_Capacity_Project_GitHub.ipynb
├── README.md
└── figures/
    ├── capacity_degradation.png
    ├── capacity_soh.png
    ├── actual_vs_predicted.png
    └── feature_correlation.png



Future Work
Extend the analysis to additional NASA battery datasets.
Test model generalization across multiple battery cells.
Investigate charge-cycle characteristics and impedance data as separate analyses.
Explore more robust forecasting approaches and evaluation strategies.
Author

Anwar Jasim
