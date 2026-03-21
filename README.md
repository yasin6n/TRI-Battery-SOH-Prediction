TRI Battery Aging & SoH Prediction 

**Dataset**: Toyota Research Institute (TRI) fast-charging LFP battery aging dataset
Available at: https://data.matr.io/1/projects/5c48dd2bc625d700019f3204  
Original publication: [^1]
(**Note:** FastCharge_000002_CH26_structure.json wasn't used in analysis because of the lack of useful data in the file)

Jupyter Notebook project for **State of Health (SoH)** prediction using this dataset.  
ITU Mathematical Engineering – Spring 2026 term project.

## Project Goal
Using the open TRI battery aging dataset, I built models to predict battery State of Health (SoH / capacity fade) based on cycle data.

## Deployment & Tools
This project was developed with **generative AI assistance** for code structuring suggestions, debugging ideas, and writing clean documentation. All scientific implementation, data processing pipelines, model training and analysis were performed by me.

**Note:** This project was originally submitted as a **MATLAB** assignment. This semester I completely rewrote it from scratch in **Python** on my own: added proper JSON → HDF5 conversion, Savitzky-Golay smoothing, feature preparation, and trained ElasticNet + Random Forest models. This allowed me to switch tools and significantly improve the quality and reproducibility of the work.

## Notebooks
| # | File                                      | Description                                                                 |
|---|-------------------------------------------|-----------------------------------------------------------------------------|
| 1 | `01_Data_Exploration.ipynb`               | Data loading, EDA, visualizations, Savitzky-Golay window optimization |
| 2 | `02_JSON_to_H5_Decoder.ipynb`             | Parse JSON files, extract `cycles_interpolated`, save into unified `.h5` |
| 3 | `03_Features_Target_Matrices.ipynb`       | Load, clean, smooth (Savitzky-Golay), prepare matrices, save ready `.h5` |
| 4 | `04_Model_Training_ElasticNet_RF.ipynb`   | Train ElasticNet & Random Forest, predict, evaluate & visualize results |

## Environment
Python 3.8+ recommended  
Dependencies listed in `requirements.txt` (includes numpy, pandas, scipy, scikit-learn, h5py, matplotlib, seaborn)
(**Note:** Python 3.12.3 has been used in a virtual environment for this project)

## How to Run
[![Open 01 in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yasin6n/TRI-Battery-SOH-Prediction/blob/main/01_Data_Exploration.ipynb)  

[![Open 02 in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yasin6n/TRI-Battery-SOH-Prediction/blob/main/02_JSON_to_H5_Decoder.ipynb)  

[![Open 03 in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yasin6n/TRI-Battery-SOH-Prediction/blob/main/03_Features_Target_Matrices.ipynb)  

[![Open 04 in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/yasin6n/TRI-Battery-SOH-Prediction/blob/main/04_Model_Training_ElasticNet_RF.ipynb)

**Locally:**
```bash
git clone https://github.com/yasin6n/TRI-Battery-SOH-Prediction.git
cd TRI-Battery-SOH-Prediction
pip install -r requirements.txt
jupyter notebook
```

## Key Results
- Achieved competitive RMSE/MAE on cycle-life prediction using ElasticNet and Random Forest
- Demonstrated clear feature importance (e.g., via coefficients and importances)
- Showed improvement after hyperparameter tuning and proper smoothing
- Prevented data leakage with causal Savitzky-Golay filtering (past data only)
- **ElasticNet**: achieved average RMSE ≈ 0.0154 (**1.54%**) and average MAE ≈ 0.0099 (**0.99%**) (normalized SoH/capacity fraction) on held-out cycles
- **Random Forest**: outperformed with average RMSE ≈ 0.0142 (**1.42%**) and average MAE = 0.0089 (**0.89%**) after hyperparameter tuning

## Visual Highlights

![Capacity Fade Trajectories](images/capacity_fade_smoothened.png)
*Capacity degradation over cycles for sample batteries*

![Elastic_Net Feature Importances](images/ENet_coefficients.png)
*Top features from Elastic Net model before/after optimization*

![Elastic_Net_Prediction Residuals](images/ENet_scatter_residuals.png)
*Scatter and Residual plot showing prediction errors for Elastic Net (last GroupKFold split)*

![Random_Forest Feature Importances](images/RF_feature_importances.png)
*Top features from Random Forest model before/after optimization*

![Random_Forest_Prediction Residuals](images/RF_scatter_residuals.png)
*Scatter and Residual plot showing prediction errors for Random Forest (last GroupKFold split)*


## Key Skills & Takeaways
- Matlab to Python transition
- Using **os** library to find the path for the json files
- Using **json** library to decode json files
- Plotting graphs with **matplotlib** and **seaborn** libraries
- Inspecting the data better and extracting more features
- Using **numpy** library to do calculations and matrix operations
- Achieving lower ram usage by using **del** command and **gc** library
- Using **h5** file with **h5py** library to save memory space and have faster data pipeline
- Using **tqdm** library to follow progress on a bar while running the code
- Using **scipy** library for preprocessing the data
- Smoothing data with **Savitzky-Golay (savgol) filter**
- Defining the savgol filter such that it only uses past data to prevent data leakage
- Setting the **windowsize** better to achieve reduced noise in data and better analysis
- Using **sklearn(Scikit-Learn)** to make data ready for analysis, define regression models and calculate the error rates
- Splitting the data with **Group K-fold** method
- Defining **Elastic Net** and **Random Forest** regressors to analyze the data and make predictions
- Inspecting the **weights** for each feature by checking **coefficients** in Elastic Net, and **feature importances** in Random Forest
- Optimizing the models by changing their **hyperparameters**
- Seeing the results by calculating **RMSE(Root Mean Squared Error)** and **MAE(Mean Absolute Error)** for model predictions
- Comparing the model performance before/after optimization by checking the error rates
- Using **pandas** library to create dataframes, to keep weights for comparison
- Comparing the weights before/after optimization on the graphs
- Visualizing the results by plotting **scatterplot** and **residuals**
- Plotting a histogram graph to check individual error rates for each group of data (batteries)

## Acknowledgments
- Toyota Research Institute for the open battery dataset
- ITU Mathematical Engineering department and instructors

## Author
**Yasin ALTIN**
**Mathematical Engineering Student @ Istanbul Technical University**
**https://linkedin.com/in/yasin-alt%C4%B1n-75b94b318** - **yasin6n06@gmail.com** → [yasin6n06@gmail.com](mailto:yasin6n06@gmail.com)

## License
MIT License

[^1]: Severson, K. A., et al. "Data-driven prediction of battery cycle life before capacity degradation." *Nature Energy* 4.5 (2019): 383-391. https://doi.org/10.1038/s41560-019-0356-8
