# Movie Recommendation System 🎬

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Library](https://img.shields.io/badge/Library-Scikit--Learn-orange)
![Library](https://img.shields.io/badge/Library-Pandas-150458)
![Status](https://img.shields.io/badge/Status-Complete-green)

A comprehensive movie recommendation engine built with Python. This project implements multiple recommendation strategies, ranging from simple popularity-based heuristics to advanced Content-Based Filtering (NLP) and Collaborative Filtering using Matrix Factorization (SVD).

The model achieves an **RMSE of 0.92**, significantly outperforming the baseline statistical approach.

## 📊 Dataset
The project uses the **MovieLens Small Dataset**, containing:
- **100,836** ratings.
- **9,742** movies.
- **610** users.
- Movie metadata (titles, genres) and user tags/timestamps.

## 🛠️ Features & Methods Implemented

### 1. Non-Personalized Recommendations (Cold Start)
- **Popularity Based:** Suggests movies with the highest view counts.
- **Weighted Rating:** Suggests movies with the highest average ratings (filtered by a minimum number of votes).

### 2. Content-Based Filtering
- **Genre Similarity:** Uses **Jaccard Similarity** to find movies with similar genre combinations (e.g., *Toy Story* ↔ *Monsters, Inc.*).
- **Text Similarity (NLP):**
  - Fetched movie plot descriptions via **TMDb API**.
  - Applied **TF-IDF Vectorization** to process text data.
  - Calculated **Cosine Similarity** to recommend movies with similar plotlines.

### 3. Collaborative Filtering
- **Item-Item Filtering:** Finds correlations between movie ratings to suggest similar items.
- **User-Based KNN:** Uses **K-Nearest Neighbors** to find users with similar taste profiles and predicts ratings based on their history.

### 4. Matrix Factorization (SVD)
- Implemented **Singular Value Decomposition (SVD)** using `scipy.sparse`.
- Handled data sparsity (98.3% sparse) by centering user ratings.
- Predicted missing ratings for unobserved user-movie pairs.

## 📈 Performance & Evaluation

To evaluate the model, I split the data into **Train (80%)** and **Test (20%)** sets, masking known ratings to calculate the error of predictions.

| Model | RMSE (Root Mean Squared Error) | Interpretation |
| :--- | :--- | :--- |
| **Baseline (Item Average)** | 0.9819 | Statistical average per movie. |
| **SVD (k=20)** | **0.9209** | **6.2% Improvement.** |

**Conclusion:** The SVD model successfully captures latent factors (user preferences and movie characteristics), resulting in an average error of less than 1 star on a 5-star scale.

## 💻 Tech Stack
- **Data Manipulation:** `pandas`, `numpy`
- **Machine Learning:** `scikit-learn`, `scipy` (SVD, Distance metrics)
- **Visualization:** `matplotlib`
- **API:** `requests` (The Movie DB)

## 🚀 How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/YOUR_USERNAME/movie-recommender-svd.git
