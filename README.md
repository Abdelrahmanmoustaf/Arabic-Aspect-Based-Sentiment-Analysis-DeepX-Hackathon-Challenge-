# Arabic Aspect-Based Sentiment Analysis (ABSA)  
## DeepX Hackathon Challenge

---

## 1. Project Overview

This project implements an Arabic Aspect-Based Sentiment Analysis (ABSA) system that extracts:

- Aspects (e.g., food, service, price)
- Sentiment per aspect (positive, negative, neutral)

from Arabic user reviews.

### Approach
The system combines:
- Advanced text preprocessing  
- Rule-based NLP  
- Machine Learning (TF-IDF + Logistic Regression)  
- Hybrid fallback strategy for robustness  

---

## 2. Dataset Description

### Input Files
```python
train_path = "DeepX_train.xlsx"
val_path = "DeepX_validation.xlsx"
unlabeled_path = "DeepX_hidden_test.xlsx"
```

### Dataset Columns
- review_id  
- review_text  
- aspects (list)  
- aspect_sentiments (dict)  
- star_rating  
- platform  
- business_category  

---

## 3. Data Analysis

### Key Insights
- Emoji-rich reviews  
- Franco-Arabic (Arabizi) usage  
- Mixed Arabic and English text  

### Data Noise
- Repeated characters  
- URLs and emails  
- Empty or punctuation-only texts  

### Engineered Features
- has_emoji  
- has_franco  
- text_len  

---

## 4. Preprocessing Pipeline

This is one of the strongest components of the system.

### Steps
- Emoji handling (extract sentiment hints)

- Franco-Arabic conversion  
  Example:
  ```
  3ayez akl -> عايز اكل
  ```

- Arabic normalization:
  - Alef: ا -> أ  
  - Yeh: ي -> ى  
  - Ta Marbuta: ه -> ة  

- Noise removal:
  - loooove -> loove  
  - Remove URLs and emails  

- Text processing:
  - Tokenization  
  - Stopword removal  
  - Light stemming  

---

## 5. Model Architecture

### Hybrid System

#### Rule-Based System
- Aspect detection using keyword dictionary  
- Sentiment detection using:
  - Lexicons (positive/negative words)  
  - Negation handling  
  - Emoji hints  
  - Star rating priors  

#### Machine Learning Model

**Aspect Detection**
- Multi-label classification  
- TF-IDF (character + word level)  
- One-vs-Rest Logistic Regression  

**Sentiment Classification**
- One classifier per aspect  
- Logistic Regression  

---

## Output Format

Generated file: `predictions.json`

```json
{
  "review_id": 123,
  "aspects": ["food", "service"],
  "aspect_sentiments": {
    "food": "positive",
    "service": "negative"
  }
}
```

---

## 6. Model Performance

### Training Results
- Train Accuracy: 96.7%  
- Validation Accuracy: 95.9%  

### Hidden Test Evaluation

| Metric    | Score |
|----------|------|
| F1 Score | 69.5% |
| Precision | 67.9% |
| Recall   | 71.1% |

Competition Score: 20.85 / 30  

---

## 7. Performance Analysis

### Strengths
- Excellent generalization (small gap between train and validation)  
- Strong handling of Arabic, Arabizi, and emojis  
- Robust hybrid system (ML + rules)  

### Weaknesses
- Moderate F1 score (~69%)  
- Aspect ambiguity  
- Limited labeled data  
- Class imbalance  
- Multi-label complexity  

---

## 8. System Features

### Supports
- Arabic text  
- Franco-Arabic (Arabizi)  
- Emojis  
- Multi-aspect reviews  

### Handles
- Noisy and informal text  
- Real-world user-generated content  

---

## 9. User Interface

Built using Gradio.

### Features
- Input: review text  
- Optional: star rating  
- Output:
  - Detected aspects  
  - Sentiment (table format)  

---

## 10. Evaluation Methodology

Metrics used:
- Exact Match Accuracy  
- Jaccard Similarity  
- Sentiment Accuracy  
- F1 / Precision / Recall  

---

## 11. Model Saving

```python
import joblib
joblib.dump(model, "absa_model.joblib")
```



