# Arabic-Aspect-Based-Sentiment-Analysis-DeepX-Hackathon-Challenge
#1. Project Overview
This project implements an Arabic Aspect-Based Sentiment Analysis ABSA
system that extracts:
Aspects (e.g., food, service, price)
Sentiment per aspect (positive, negative, neutral)
from Arabic user reviews.
The system combines:
🔹 Advanced text preprocessing
🔹 Rule-based NLP
🔹 Machine Learning TF IDF  Logistic Regression)
🔹 Hybrid fallback strategy for robustness
#2.  Dataset Description
Input Files
train_path = "DeepX_train.xlsx"
val_path   
= "DeepX_validation.xlsx"
unlabeled_path = "DeepX_hidden_test.xlsx"
Columns
review_id
review_text
aspects
 (list)
aspect_sentiments
 (dict)
star_rating
platform
business_category
#3.  Data Analysis
Key Insights
Presence of emoji-rich reviews
Significant Franco-Arabic Arabizi) usage
Mixed language Arabic + English)
Noise:
Repeated characters
URLs, emails
Empty / punctuation-only texts
Engineered Features
has_emoji
has_franco
text_len
#4.  Preprocessing Pipeline
The preprocessing is one of the strongest parts of your solution.
Steps:
Emoji Handling
Extract sentiment hints (positive / negative / neutral)
Franco-Arabic Conversion
Example:
"3ayez akl" → "ﻋﺎﻳﺰ اﻛﻞ"
Arabic Normalization
Normalize:
Alef forms (ا

 
→
 
أ
)
Yeh (ي

 
→
 
ى
)
Ta marbuta (ه

 
→
 
ة
)
Noise Removal
Remove:
Repeated characters (loooove 
→
 loove)
URLs, emails
Tokenization
Stopword Removal
Light Stemming
#5.  Model Architecture
🔷 Hybrid System
A) Rule-Based System
Aspect detection using keyword dictionary
Sentiment using:
Lexicons (positive/negative words)
Negation handling
Emoji hints
Star rating priors
B) Machine Learning Model
1. Aspect Detection
Multi-label classification
Model:
TF-IDF (char + word)
OneVsRest Logistic Regression
2. Sentiment Classification
One classifier per aspect
Model:
Logistic Regression
 Output Format
Generated file:
predictions.json
Example:
{
}
"review_id": 123,
"aspects": ["food", "service"],
"aspect_sentiments": {
"food": "positive",
"service": "negative"
}
6.  Model Performance
Training Results
Train Accuracy: 96.7%
Validation Accuracy: 95.9%
Final .json evaluation metrics for hidden_test
Metric
F1 Score
Precision
Recall
Score
69.5%
67.9%
71.1%
Competition Score
Pillar 1 20.85 / 30
7. Performance Analysis
🔹 Strengths
Excellent generalization (small gap between train & validation)
Strong handling of:
Arabic text
Franco-Arabic
Emojis
Robust hybrid system ML + rules)
🔸 Weaknesses
Moderate F1 score (
≈
69%
Possible issues:
Aspect ambiguity
Limited labeled data per aspect
Class imbalance
Multi-label complexity
8.  System Features
Supports:
Arabic text 
Franco-Arabic Arabizi)
Emojis 😊🔥💔
Multi-aspect reviews
Handles:
Noise & informal text
Real-world user-generated content
6.  User Interface
Built using Gradio:
Features:
Input review
Optional star rating
Output:
Aspects
Sentiments (table format)
9.  Evaluation Methodology
Metrics used:
Exact Match Accuracy
Jaccard Similarity
Sentiment Accuracy
F1 / Precision / Recall
10.  Model Saving
joblib.dump(model, "absa_model.joblib")
