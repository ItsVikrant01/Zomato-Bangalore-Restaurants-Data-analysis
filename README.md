# 🍽️ Zomato Bangalore Restaurants — Data Analysis & Power BI Dashboard

A complete end-to-end data analytics project that explores Bengaluru's restaurant scene using Python for data cleaning & sentiment analysis, and Power BI for interactive visual storytelling.

---

## 📌 Short Description / Purpose

The Zomato Bangalore Restaurants Dashboard is a visually engaging and analytical Power BI report designed to help users explore and compare thousands of restaurants across Bengaluru's neighborhoods. It focuses on key restaurant attributes like cuisine type, dish popularity, ratings, cost for two, restaurant type, and customer sentiment — all in one interactive, drill-through experience. This tool is intended for use by food enthusiasts, restaurant owners, investors, and data-driven strategists who want to understand Bengaluru's food industry landscape.

---

## 🔧 Tech Stack

The project was built using the following tools and technologies:

- 🐍 **Python (Jupyter Notebook)** — Core language for data cleaning, transformation, and sentiment analysis
- 🐼 **Pandas & NumPy** — Data manipulation and numerical operations
- 🤖 **Scikit-learn (KNNImputer + StandardScaler)** — Smart imputation for missing rating values using K-Nearest Neighbors with feature scaling
- 💬 **NLTK VADER** — Sentiment analysis on customer reviews to classify restaurant sentiment as Positive, Neutral, or Negative
- 📊 **Power BI Desktop** — Main data visualization platform used for report/dashboard creation
- ⚙️ **Power Query** — Data transformation and loading layer within Power BI
- 📐 **DAX (Data Analysis Expressions)** — Used for calculated measures, dynamic visuals, and conditional logic
- 🔗 **Data Modeling** — Relationships established among multiple tables (`main data`, `Rest_type`, `Dish_liked`, `Cuisine`) to enable cross-filtering and drill-through
- 📁 **File Formats** — `.ipynb` for Python notebook, `.csv` for cleaned output files, `.pbix` for the Power BI dashboard

---

## 📂 Data Source

**Source:** [Kaggle — Zomato Bangalore Restaurants by Himanshu Poddar](https://www.kaggle.com/datasets/himanshupoddar/zomato-bangalore-restaurants)

The dataset contains information on approximately **45,000+ restaurants** in Bengaluru, including details on:

- Restaurant name, location/neighborhood
- Cuisine types offered
- Dishes liked by customers
- Restaurant type (Delivery, Dine-out, Buffet, Cafes, etc.)
- Online ordering & table booking availability
- Approximate cost for two people
- Ratings (out of 5) & number of votes
- Customer reviews list

---

## ✨ Features / Highlights

### 🔴 Business Problem

Bengaluru's restaurant industry is one of the most competitive in India. With over 45,000 restaurants — and new ones opening every day — it has become increasingly difficult for new entrants to compete with already established places. Key challenges include high real estate costs, rising food costs, shortage of quality manpower, and over-licensing. Restaurant owners and investors often lack a clear, data-driven view of which locations, cuisines, and price points perform best.

### 🎯 Goal of the Dashboard

To provide a single interactive platform where restaurant owners, investors, and food enthusiasts can:
- Discover which cuisine types and specific dishes dominate particular areas of Bengaluru
- Understand how ratings and costs are distributed across neighborhoods
- Analyze customer sentiment (Positive / Neutral / Negative) derived from real reviews
- Identify the most popular restaurant types by location
- Make data-backed decisions around menu planning, location selection, and pricing strategy

---

## 🖥️ Walk-through of Key Visuals

### 1. 🗂️ Cuisine Drill-Through Table *(2-Level Hierarchy)*
An interactive table showing cuisine distribution across Bengaluru. Clicking on a **cuisine type** (e.g., "North Indian") drills down to show the **specific dishes** most liked under that cuisine in a selected area or city. This two-level hierarchy makes it easy to go from broad cuisine categories to granular dish-level insights.

### 2. 📍 Restaurant Distribution by Location
A visual breakdown of how many restaurants exist across Bengaluru's different neighborhoods, helping identify high-density food zones.

### 3. ⭐ Ratings & Cost Analysis
Visuals comparing average restaurant ratings and approximate cost for two people across locations and restaurant types, letting users spot value-for-money areas.

### 4. 💬 Sentiment Analysis Overview
Customer reviews were processed using NLTK's VADER sentiment analyzer. Each restaurant is labeled as **Positive**, **Neutral**, or **Negative** based on aggregated review scores. The dashboard shows sentiment distribution across the city.

### 5. 🍴 Restaurant Type Breakdown
A chart showing what kinds of dining experiences (Delivery, Dine-out, Buffet, Café, etc.) are most common across different parts of Bengaluru.

### 6. 🥘 Dishes Liked Across Neighborhoods
A filtered view of the most popular dishes liked by customers — connected to the cuisine drill-through — giving a street-level picture of food preferences.

---

## 🧹 Data Cleaning & Preparation (Python)

The raw Kaggle data required significant cleaning before it could be used in Power BI. Here is what was done in the Jupyter Notebook (`Zomatodata.ipynb`):

1. **Duplicate Removal** — Identified and removed duplicate rows
2. **Cost Column Cleaning** — Removed comma separators (e.g., `1,000` → `1000`) and converted to integer
3. **Missing Cost Values** — Filled NaN values using **location-wise median** to preserve geographic context
4. **Rating Column Cleaning** — Removed `/5` suffixes and converted to numeric format
5. **KNN Imputation for Ratings** — Used `KNNImputer` with `StandardScaler` (applied to `rate`, `votes`, and `approx_cost`) to intelligently fill missing rating values rather than using a simple mean/median
6. **Review Text Extraction & Cleaning** — Parsed raw review strings, removed noise (URLs, encoding artifacts, RATED markers), and prepared clean text for sentiment analysis
7. **VADER Sentiment Analysis** — Scored each restaurant's reviews sentence by sentence, then computed average sentiment, min/max scores, and positive/negative/neutral percentages per restaurant
8. **Column Splitting for Power BI** — Columns like `cuisines`, `dish_liked`, and `rest_type` contained list values. These were exploded into separate normalized tables:
   - `Cuisine.csv` — one row per cuisine per restaurant
   - `Dish_liked.csv` — one row per dish per restaurant
   - `Rest_type.csv` — one row per restaurant type per restaurant
9. **Encoding Fix** — Fixed latin1/UTF-8 encoding issues in restaurant names
10. **Final Export** — Saved `Zomato_cleaned_data.csv` along with the three lookup tables

---

## 💡 Business Impact & Insights

- **Restaurant Owners** can identify which cuisines and dishes are trending in their locality and adjust menus accordingly
- **New Entrepreneurs** can spot under-served neighborhoods with high potential and lower competition
- **Investors** can evaluate neighborhoods based on average ratings, cost brackets, and sentiment scores before backing a restaurant
- **Food Enthusiasts** can discover top-rated spots by dish type or cuisine anywhere in Bengaluru

---

## 📁 Repository Structure

```
📦 Zomato-Bangalore-Dashboard
 ┣ 📓 Zomatodata.ipynb          # Python notebook: data cleaning + sentiment analysis
 ┣ 📊 Dashboard.pbix             # Power BI dashboard file
 ┣ 📄 Zomato_cleaned_data.csv   # Main cleaned dataset (output)
 ┣ 📄 Cuisine.csv                # Exploded cuisine lookup table
 ┣ 📄 Dish_liked.csv             # Exploded dish liked lookup table
 ┣ 📄 Rest_type.csv              # Exploded restaurant type lookup table
 ┗ 📸 screenshots/               # Dashboard preview images
```

---

## 🚀 How to Run

### Python Notebook
1. Install required libraries:
   ```bash
   pip install pandas numpy scikit-learn nltk itables
   ```
2. Download VADER lexicon:
   ```python
   import nltk
   nltk.download('vader_lexicon')
   ```
3. Place `zomato.csv` (from Kaggle) in the same folder as the notebook
4. Run all cells in `Zomatodata.ipynb` — this will generate the cleaned CSV files

### Power BI Dashboard
1. Open `Dashboard.pbix` in **Power BI Desktop**
2. Update the data source path to point to your locally generated CSV files
3. Click **Refresh** to load the latest data
4. Use the **Cuisine drill-through table** to explore by cuisine → then click into a cuisine to see specific popular dishes

---

## 📸 Screenshots / Demo
![Dashboard Preview](screenshots/Dashboard%20SS.png)

> **Dashboard Features Visible:**
> - 🔴 Top filters — Cities, Restaurant Type, Book Table, Online Order
> - 📊 Cuisine-to-Dish Popularity Drilldown (click any cuisine to see specific dishes)
> - 💬 Do Ratings Reflect Customer Opinion? (Scatter: Rating vs Avg Sentiment)
> - 💸 Do Expensive Restaurants Deliver Better Experiences? (Cost vs Sentiment)
> - 💎 Hidden Gems Worth Discovering (high sentiment, lower votes)
> - 🏆 Top Performing Restaurants (high rating + high sentiment)
> - ⚠️ Overhyped Restaurants (high rating but low sentiment)
> - KPI Cards — Avg Rating (3.66) | Avg Cost for 2 (₹588.70) | Avg Sentiment (0.26) | Avg Voting (330.80) | No. of Restaurants (44,054)

---

## 🙌 Acknowledgements

- Dataset by [Himanshu Poddar on Kaggle](https://www.kaggle.com/datasets/himanshupoddar/zomato-bangalore-restaurants)
- Sentiment analysis powered by [NLTK VADER](https://www.nltk.org/api/nltk.sentiment.vader.html)
