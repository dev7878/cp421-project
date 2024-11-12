---
### **Project Report: Book Recommendation System**

#### **1. Introduction**

The goal of this project was to build a recommendation system for books, leveraging user ratings data. The system utilizes various models, from simple averages to collaborative filtering techniques, to predict ratings and recommend books. The performance of each model was evaluated using Root Mean Square Error (RMSE) and other relevant metrics.
---

### **2. Data Loading and Initial Inspection**

- **Files Loaded**: `Users.csv`, `Books.csv`, and `Ratings.csv` were loaded.
- **Summary**: Basic information about the datasets, including column types, missing values, and sample records, was displayed to understand the structure.
- **Key Findings**:
  - The `Users` dataset had missing values in the `Age` column.
  - The `Books` dataset contained mixed data types in `Year-Of-Publication` and some missing values in author and publisher fields.
  - The `Ratings` dataset was complete and primarily consisted of integer ratings.

---

### **3. Data Cleaning**

- **Users Data**: Missing ages were filled with the median age, and outliers (ages below 10 or above 100) were removed.
- **Books Data**: Non-numeric `Year-Of-Publication` values were coerced into numeric format, and invalid entries were removed. Missing `Book-Title` entries were dropped.
- **Ratings Data**: Only explicit ratings (those greater than 0) were retained to focus on meaningful feedback.
- **Output**: Cleaned datasets were displayed, confirming that each dataset was prepared for further analysis.

---

### **4. Exploratory Data Analysis (EDA)**

- **User Demographics**:
  - **Age Distribution**: Most users were concentrated in the 20-40 age range.
  - **Top Locations**: The United States had the most active users.
- **Book Data**:
  - **Publication Year**: The majority of books were published between 1990 and 2005.
  - **Top Rated Books**: A bar chart highlighted the books with the most ratings.
- **Ratings Analysis**:
  - **Rating Distribution**: Ratings were mostly high (above 5), indicating a positive bias in the data.
  - **Ratings Per User**: Most users had rated fewer than 10 books, suggesting that the dataset was sparse.

---

### **5. Data Splitting**

- **Method**: The data was split into training (80%) and test (20%) sets to evaluate model performance on unseen data.
- **Output**: Training data size was 346,936 and test data size was 86,735, ensuring a sufficient sample for both model training and validation.

---

### **6. Baseline Models**

- **Global Mean Model**:
  - **Method**: Predicted all ratings as the average rating across the dataset.
  - **RMSE**: 1.8503
- **User Mean Model**:
  - **Method**: Predicted ratings based on each user's average rating.
  - **RMSE**: 1.6964
- **Item Mean Model**:
  - **Method**: Predicted ratings based on each book's average rating.
  - **RMSE**: 1.9527
- **Findings**: The User Mean Model had the lowest RMSE among the baseline models, indicating it provided a better fit than global or item-level averages.

---

### **7. Collaborative Filtering with Matrix Factorization (ALS)**

- **Method**: The ALS (Alternating Least Squares) model was implemented to learn latent factors for users and books, predicting ratings based on the dot product of these factors.
- **RMSE**: 5.0801, indicating a relatively high error due to sparsity and limited tuning.
- **Challenges**: Installation issues with initial libraries led to the use of the `implicit` library for ALS, and performance was affected by high sparsity in the user-item matrix.

---

### **8. Improving the ALS Model**

- **Filtering Sparse Users and Items**: Users and items with fewer than five ratings were removed, resulting in a denser dataset for ALS.
- **Parameter Tuning**: The ALS model was re-trained with higher factors, reduced regularization, and additional iterations.
- **Hybrid Approach**: For unknown users or items, the system fell back on the User Mean or Item Mean predictions.
- **Hybrid ALS Model RMSE**: 1.8611, a significant improvement over the initial ALS model, showcasing the effectiveness of filtering and hybridization.

---

### **9. Evaluation and Additional Metrics**

- **Threshold (7) for "Liked" Ratings**:
  - **Precision**: 0.8188, indicating the percentage of recommended items that were relevant.
  - **Recall**: 0.8514, representing the proportion of relevant items successfully recommended.
  - **F1 Score**: 0.8348, a balanced metric between precision and recall.
- **Threshold Tuning**:
  - Threshold 6 increased recall but slightly decreased precision, while threshold 8 had the opposite effect. Threshold 7 provided a balanced F1 Score, making it the optimal choice.

---

### **10. Model Performance Comparison**

- A table compared all models:
  - **Global Mean RMSE**: 1.8503
  - **User Mean RMSE**: 1.6964
  - **Item Mean RMSE**: 1.9527
  - **ALS RMSE**: 5.0801
  - **Hybrid ALS RMSE**: 1.8611 (Precision: 0.8188, Recall: 0.8514, F1: 0.8348)
- **Conclusion from Comparison**: The Hybrid ALS model, with optimized parameters and a fallback approach, performed best among advanced models, while the User Mean model was the best among baselines.

---

### **11. Sample Recommendations**

- **Method**: For sample users, top recommendations were generated based on ALS latent factors.
- **Examples**:
  - User 26 received recommendations like _"Whirlwind (The X-Files)"_ and _"A Lady of His Own"_.
  - User 6 was not found in the model, highlighting a limitation when users lack interaction data.
- **Insight**: The recommendations appeared diverse, covering various genres and styles, which aligns with the system’s goal to provide personalized suggestions.

### Workflow

1. ![UI Screenshot](workflow\Recommendation-System-Workflow-1.png)
2. ![UI Screenshot](workflow\Recommendation-System-Workflow-full.png)

---

### **Conclusion**

This project successfully developed a book recommendation system using both baseline models and collaborative filtering. The Hybrid ALS model, with its use of latent factors and fallback mechanisms, emerged as the best-performing model. The model tuning and filtering significantly reduced RMSE, making the recommendations both accurate and relevant. Further analysis revealed that threshold tuning could improve the balance between precision and recall, optimizing user satisfaction.

**Key Findings**:

1. The User Mean model outperformed simple baselines, while ALS alone had limitations due to data sparsity.
2. The Hybrid ALS model achieved the best results by combining matrix factorization with fallback mechanisms, demonstrating robust performance.
3. Threshold tuning (threshold = 7) provided an ideal balance between precision and recall, ensuring quality recommendations without overwhelming users.

**Future Work**: Additional improvements could involve incorporating contextual features like genre or publication year, or using deep learning-based collaborative filtering to further enhance recommendations.

--
