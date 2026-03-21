# TRI Battery Aging & SoH Prediction 

Jupyter Notebook project for **State of Health (SoH)** prediction using the Toyota Research Institute (TRI) battery aging dataset.  
ITU Mathematical Engineering – Spring 2026 term project.

## Project Goal
Using the open TRI battery aging dataset, I built models to predict battery State of Health (SoH / capacity fade) based on cycle data.

**Note:** This project was originally submitted as a **MATLAB** assignment. This semester I completely rewrote it from scratch in **Python** on my own: added proper JSON → HDF5 conversion, Savitzky-Golay smoothing, feature preparation, and trained ElasticNet + Random Forest models. This allowed me to switch tools and significantly improve the quality and reproducibility of the work.

## Notebooks

| # | File                                      | Description                                                                 |
|---|-------------------------------------------|-----------------------------------------------------------------------------|
| 1 | `01_Data_Exploration.ipynb`               | Data loading, EDA, visualizations, Savitzky-Golay window optimization |
| 2 | `02_JSON_to_H5_Decoder.ipynb`             | Parse JSON files, extract `cycles_interpolated`, save into unified `.h5` |
| 3 | `03_Features_Target_Matrices.ipynb`       | Load, clean, smooth (Savitzky-Golay), prepare matrices, save ready `.h5` |
| 4 | `04_Model_Training_ElasticNet_RF.ipynb`   | Train ElasticNet & Random Forest, predict, evaluate & visualize results |

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
