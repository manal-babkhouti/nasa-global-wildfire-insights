# 🔥 NASA Global Wildfire Insights

This project presents a comprehensive data science analysis of global wildfire activity during 2024 using satellite data from NASA’s FIRMS (Fire Information for Resource Management System). It combines geospatial exploration, classification modeling, and unsupervised learning to understand when, where, and how fires occur — and whether satellite data can predict or uncover hidden patterns.

---

## 📌 Objectives

- Analyze global fire detections in 2024 using MODIS satellite data.
- Uncover spatio-temporal patterns in wildfire activity.
- Assess fire intensity and confidence levels.
- Build classification models to predict fire confidence.
- Apply dimensionality reduction (PCA, t-SNE) to explore class separability.
- Use KMeans clustering to identify latent groupings in fire events.

---

## 📊 Methodology

- **Data Preprocessing**: Cleaned, encoded, and sampled over 100,000 fire records.
- **Supervised Learning**: Trained a `RandomForestClassifier` to predict fire confidence class.
- **Dimensionality Reduction**: Applied `PCA` and `t-SNE` to visualize separability.
- **Clustering**: Used `KMeans` in embedded spaces to explore natural groupings.
- **Evaluation**: Assessed models via precision/recall/F1-score and adjusted Rand index.

---

## ✅ Key Insights

- Some satellite features show clear correlation with fire confidence.
- The Random Forest model achieved meaningful classification performance.
- PCA and t-SNE revealed overlap between fire classes, hinting at complexity in feature space.
- Clustering yielded low alignment with true classes — showing unsupervised learning alone may not capture fire confidence without supervision.

---

## 📎 Files Included

- `NASA_FIRMS_Wildfire_Analysis.ipynb` — Full notebook with EDA, modeling & clustering.
- `NASA_FIRMS_Global_Wildfire_Insights_Report.pdf` — A detailed LaTeX report (with figures and commentary).
- `requirements.txt` — List of Python dependencies for easy setup.

---

## 🧠 Why This Project Matters

This project demonstrates the ability to:
- Handle large-scale satellite data with real-world relevance.
- Combine supervised and unsupervised techniques.
- Interpret ML results in context, with rigorous evaluation.
- Communicate findings clearly in a professional data science report.

---

## 📥 How to Use

Clone the repo, install the requirements, and open the notebook:

```bash
git clone https://github.com/manal-babkhouti/nasa-global-wildfire-insights.git
cd nasa-global-wildfire-insights
pip install -r requirements.txt
jupyter notebook NASA_FIRMS_Wildfire_Analysis.ipynb



## 📘 Read the Full Report

👉 The complete report (with visuals, interpretations, and deep analysis) is available here:  
📄 [View the Full PDF Report](https://github.com/manal-babkhouti/nasa-global-wildfire-insights/raw/main/NASA_FIRMS_Global_Wildfire_Insights_Report.pdf)  
This is the full write-up explaining the project's context, methods, results, and key insights.
