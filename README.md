# Hierarchical Categorization of Digikala Items

## Overview
This project focuses on categorizing Digikala items hierarchically, from coarse to fine-grained categories across three levels. The classification model leverages ParsBERT, with a Multi-Layer Perceptron (MLP) trained on top of the CLS output token for final classification.

## Dataset
The dataset consists of items from **Digikala**, an online marketplace. Each item is labeled with hierarchical categories to facilitate structured classification.

### Dataset Overview
- **Total Size**: 529,322 items  
- **Unique Categories**:  
  - **First Level**: 11 categories  
  - **Second Level**: 96 categories  
  - **Third Level**: 682 categories  


## Methodology
The general approach is to add an **MLP layer** on top of the **CLS token** from the pre-trained **ParsBERT** model and fine-tune the model for each category level.

### Multi-Level Classification Approach

#### **Level 1 Classification**  
- **Input**: The **name of the item**.  
- **Output**: The predicted **first-level category**.

#### **Level 2 Classification**  
- **Training Phase**:  
  - The model receives the **concatenation of the item name and the actual first category**.  
  - It is trained to predict the **second-level category**.  
- **Testing Phase**:  
  - The **Level-1 model** is used to predict the first category.  
  - The **predicted first category** is concatenated with the item name.  
  - This concatenated input is passed to the **Level-2 model** to predict the second category.

#### **Level 3 Classification**  
- **Training Phase**:  
  - The model receives the **concatenation of the item name, actual first category, and actual second category**.  
  - It is trained to predict the **third-level category**.  
- **Testing Phase**:  
  - The **Level-1 model** predicts the first category.  
  - The **predicted first category** is concatenated with the item name and passed to the **Level-2 model** to predict the second category.  
  - The **item name, predicted first category, and predicted second category** are concatenated and passed to the **Level-3 model** to predict the third category.  


## Results
The model achieves high accuracy in classifying Digikala items into their respective hierarchical categories. Detailed results and performance metrics are shown in the table below.

| Level  | Accuracy | F1 Score |
|--------|----------|----------|
| Level 1 | 0.9843   | 0.9842   |
| Level 2 | 0.9733   | 0.9732   |
| Level 3 | 0.9576   | 0.9563   |

To evaluate the generalization performance of the model on another dataset, I crawled data from the **Torob** website for the first category and tested the model on this dataset. The results are shown below:

| Dataset | Accuracy | F1 Score |
|---------|----------|----------|
| Torob (Level 1) | 0.9280   | 0.9424   |