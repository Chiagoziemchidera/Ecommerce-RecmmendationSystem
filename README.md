# Ecommerce-recommendation-system

A machine learning–powered **Product Recommendation System** built to help e-commerce platforms deliver personalized product suggestions.  
By analyzing browsing patterns, ratings, and purchase behavior, the system uses **collaborative filtering** and **content-based filtering** to recommend items users are most likely to enjoy.  
The goal: **improve user experience and boost conversions for online sellers.**

---

## ❄️ Cold Start Problem

The **cold start problem** occurs when a recommender system lacks enough data to make meaningful suggestions. It appears in two main forms:

### **Types of Cold Start**
- **User Cold Start:** A new user has no interaction history.
- **Item Cold Start:** A newly added item has no ratings or interactions.

---

## 🔧 How to Handle the Cold Start Problem

### **1. Rank-Based Recommendations**
Suggest popular or highly rated items for new users when no personalized data exists.

### **2. Content-Based Filtering**
Recommend new items by analyzing their attributes or metadata, matching them to users with similar tastes.

### **3. Hybrid Methods**
Combine collaborative filtering, content-based filtering, and popularity-based methods for more robust performance.

---

## 📝 Examples

- **User Cold Start:** Use collaborative filtering to find similar users and recommend items they liked.  
- **Item Cold Start:** Use content-based filtering to match the item’s features with user preferences.  
- **Hybrid Approach:** Blend methods to reduce limitations of any single strategy.

---

## 📊 Dataset

The project uses an Amazon electronics ratings dataset.  
Since the data has no headers, each user and product is assigned a unique numeric ID to avoid bias and preserve anonymity.

- Dataset link:  
  https://www.kaggle.com/datasets/vibivij/amazon-electronics-rating-datasetrecommendation/download?datasetVersionNumber=1

---

## 🚀 Approach

### 1. **Rank-Based Product Recommendation**

**Objective**
- Recommend products with the highest number of ratings  
- Provide popular items for new users (Cold Start Problem)  
- Improve initial recommendations

**Output**
- Top **5 products** with at least **50 or 100 interactions**

**Method**
- Calculate average rating per product  
- Count total number of ratings  
- Combine metrics into a DataFrame and sort by rating  
- Build a function to return the top *n* products based on interaction thresholds

---

### 2. **Similarity-Based Collaborative Filtering**

**Objective**
- Provide personalized recommendations using behavior of similar users

**Output**
- Top **5 recommended products** based on similar user interactions

**Method**
- Convert `user_id` from object to integer (0–1539)  
- Create a function to find similar users:  
  - Compute cosine similarity for the target user  
  - Sort users by similarity score  
  - Exclude the target user  
- Create a recommendation function:  
  - Identify products the target user has already interacted with  
  - Recommend products highly interacted with by similar users but not the target user

---

### 3. **Model-Based Collaborative Filtering (SVD)**

**Objective**
- Generate personalized suggestions using matrix factorization  
- Address scalability and data sparsity issues in user–item matrices

**Output**
- Top **5 product recommendations** per user

**Method**
- Convert the interaction matrix to a **CSR (Compressed Sparse Row)** matrix  
- Apply **Singular Value Decomposition (SVD)** to reduce data into **50 latent factors**  
- Reconstruct predicted ratings using: `U × Σ × Vᵀ`  
- Store predicted ratings in a DataFrame aligned with the original matrix  
- Build a recommendation function to:  
  - Combine actual and predicted ratings for a user  
  - Filter out rated items  
  - Sort by predicted rating  
  - Return the top recommended products

**Model Evaluation**
- Calculate average actual vs predicted ratings  
- Store in an `rmse_df` DataFrame  
- Compute **RMSE** to measure accuracy of the SVD model
