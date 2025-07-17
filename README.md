# -BeautyBytes
## 📌 Project Summary

**BeautyBytes** is a full-cycle data analytics project aimed at uncovering trends, customer preferences, and brand insights in the online cosmetics industry using a dataset of 15,000 makeup products. The project includes:

✅ Market research & sales trend analysis  
✅ Content-based recommendation system  
✅ Brand performance & customer feedback analysis  
✅ Behavioral segmentation for targeted marketing  
✅ End-to-end Power BI dashboard

---

## 🧰 Tools Used

- Python (Pandas, Seaborn, Scikit-learn, TfidfVectorizer)
- Power BI (for executive visuals & trends)
- Google Colab Notebook
- Cosmetology product dataset with 14 features

---

### 📊 1. Exploratory Data Analysis (EDA)
- Most common product categories: Serum, Mascara, Face Oil
  <img width="850" height="474" alt="image" src="https://github.com/user-attachments/assets/84be26dd-43a5-48d3-b4f8-592c6f755c27" />
- Ingredient popularity: Glycerin, Retinol, Vitamin C
  <img width="839" height="466" alt="image" src="https://github.com/user-attachments/assets/ec4c2fbe-a80a-4ec0-8778-db69a233c081" />
- Highest rated skin-type focus: **Combination & Oily**
  <img width="704" height="393" alt="image" src="https://github.com/user-attachments/assets/393e39cf-1d80-4d3e-82d6-67d162116bfe" />
- Highest Products sold in : Italy, USA
  <img width="859" height="449" alt="image" src="https://github.com/user-attachments/assets/3bfd14bf-3572-4020-aa0c-5c347ec87159" />
- Packaging Type Preferred: Jar
  <img width="704" height="393" alt="image" src="https://github.com/user-attachments/assets/ce0b8c4d-aa90-4342-bec4-b7c78f7ef65c" />

### 🧠 2. Recommendation Engine
- Uses category, main ingredient, skin type & packaging
- Built using TF-IDF and cosine similarity
- Returns 5 similar products for any selected item
   
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

# Combine relevant text columns
df['Combined_Features'] = df['Category'] + ' ' + df['Main_Ingredient'] + ' ' + df['Skin_Type'] + ' ' + df['Packaging_Type']
# Vectorize
tfidf = TfidfVectorizer()
tfidf_matrix = tfidf.fit_transform(df['Combined_Features'])
# Cosine similarity
cosine_sim = cosine_similarity(tfidf_matrix)
def recommend(product_name, top_n=5):
    idx = df[df['Product_Name'] == product_name].index[0]
    sim_scores = list(enumerate(cosine_sim[idx]))
    sim_scores = sorted(sim_scores, key=lambda x: x[1], reverse=True)[1:top_n+1]
    recommended = df.iloc[[i[0] for i in sim_scores]]['Product_Name'].tolist()
    return recommended
    print('A user who likes Ultra Face Mask might also enjoy products with similar skin-type targets and ingredients such as: ',recommend('Ultra Face Mask'))
A user who likes Ultra Face Mask might also enjoy products with similar skin-type targets and ingredients such as:  
['Magic Foundation', 'Super Cc Cream', 'Ultra Foundation', 'Ultra Eye Shadow', 'Divine Face Mask']
### 🔍 3. Brand Popularity & Feedback
- Popularity score: Rating × log(Number of Reviews)
- Brands like **HourGlass, Milk Makeup, Becca** lead in satisfaction
  # Create popularity score
import numpy as np
df['Popularity_Score'] = df['Rating'] * np.log1p(df['Number_of_Reviews'])

# Brand-wise Aggregates
brand_stats = df.groupby('Brand')[['Rating', 'Number_of_Reviews', 'Popularity_Score']].mean().sort_values(by='Popularity_Score', ascending=False)

# Top 10 Popular Brands
brand_stats.head(10)
<img width="1407" height="306" alt="Capture" src="https://github.com/user-attachments/assets/b1bb5368-74f5-4157-a9a1-07d881709539" />

---

## 📊 Power BI Dashboard

**📁 Pages:**

### 🟦 PAGE 1: Executive Overview
- Treemap: Brand dominance
- Barplot : Category vs Rating
- Bubble chart: Price vs Rating vs Review count
- Donut: Product origin distribution
  <img width="1042" height="831" alt="image" src="https://github.com/user-attachments/assets/2c2fb585-326a-4aeb-95c0-e294ad5e3c28" />
  
### 🟨 PAGE 2: Product Performance and Behavorial insights
- Barplot: Usage frequency vs rating
- Skin type × category distribution
- Skin type x average rating
  <img width="1041" height="838" alt="image" src="https://github.com/user-attachments/assets/ca2b75a4-17a7-4e0c-a748-d38fcdac4914" />

### 🟥 PAGE 3: Global Trends & Ethics
- Country vs Avg Rating & Price
- Cruelty-Free share by country
- Ingredient rating heatmap
  <img width="1037" height="844" alt="image" src="https://github.com/user-attachments/assets/33ec63ad-cb91-4c81-88d6-264e7863aea4" />

### 🟩 PAGE 4: Supporting Analysis
- Packaging type breakdown
- Common product sizes
- Gender targeting distribution
  <img width="1049" height="840" alt="image" src="https://github.com/user-attachments/assets/7acd411c-20dc-43e0-b068-83f03da26e31" />

## 📌 Key Business Insights

- **Italy & USA** lead in product volume, but **Japan & France** offer higher-rated items  
- **Retinol** and **Glycerin** are most associated with high ratings  
- **Daily-use products** are more affordable and receive more reviews  
- **Cruelty-free products** show higher pricing and better customer feedback  
- **Sensitive-skin products** are the highest rated across the board

---

## 📥 Files in Repo

- `💄_BeautyBytes_...ipynb` → Full notebook with EDA + ML
- `Makeup-Sales-Trend-Analysis.pdf` → Power BI dashboard export
- `beauty_products_clean.csv` → Preprocessed data
- `README.md` → This file

---
## 🚀 Future Work

- Integrate real-time reviews via Sephora API  
- Add NLP sentiment scoring on actual text reviews  
- Deploy recommendation engine with Streamlit or Flask

---

## 🤝 Let’s Connect!

If you're a data team, beauty brand, or just love analytics & ecommerce — let’s talk!  
📧 Email • 💼 LinkedIn • 🧠 Portfolio
