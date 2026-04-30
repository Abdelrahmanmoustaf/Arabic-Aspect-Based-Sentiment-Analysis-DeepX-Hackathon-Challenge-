# Arabic-Aspect-Based-Sentiment-Analysis-DeepX-Hackathon-Challenge
📌 1. Project Overview

This project implements an Arabic Aspect-Based Sentiment Analysis (ABSA) system that extracts:

Aspects (e.g., food, service, price)
Sentiment per aspect (positive, negative, neutral)

from Arabic user reviews.

🚀 Approach

The system combines:

🔹 Advanced text preprocessing
🔹 Rule-based NLP
🔹 Machine Learning (TF-IDF + Logistic Regression)
🔹 Hybrid fallback strategy for robustness
📊 2. Dataset Description
📂 Input Files
train_path = "DeepX_train.xlsx"
val_path = "DeepX_validation.xlsx"
unlabeled_path = "DeepX_hidden_test.xlsx"
🧾 Dataset Columns
review_id
review_text
aspects (list)
aspect_sentiments (dict)
star_rating
platform
business_category
🔍 3. Data Analysis
📈 Key Insights
Presence of emoji-rich reviews 😊🔥💔
Significant Franco-Arabic (Arabizi) usage
Mixed language (Arabic + English)
⚠️ Data Noise
Repeated characters
URLs & emails
Empty / punctuation-only texts
🧠 Engineered Features
has_emoji
has_franco
text_len
🧹 4. Preprocessing Pipeline

This is one of the strongest components of the system.

🔧 Steps
😀 Emoji Handling
Extract sentiment hints (positive / negative / neutral)
🔤 Franco-Arabic Conversion

Example:

"3ayez akl" → "عايز اكل"
✍️ Arabic Normalization

Normalize:

Alef forms: ا → أ
Yeh: ي → ى
Ta Marbuta: ه → ة
🧽 Noise Removal

Repeated characters:

loooove → loove
URLs, emails
🔡 Text Processing
Tokenization
Stopword removal
Light stemming
🤖 5. Model Architecture
🔷 Hybrid System
🅰️ Rule-Based System
Aspect detection using keyword dictionary
Sentiment detection using:
Lexicons (positive/negative words)
Negation handling
Emoji hints
Star rating priors
🅱️ Machine Learning Model
1. Aspect Detection
Multi-label classification
Model:
TF-IDF (character + word level)
One-vs-Rest Logistic Regression
2. Sentiment Classification
One classifier per aspect
Model:
Logistic Regression
📤 Output Format

Generated file: predictions.json

{
  "review_id": 123,
  "aspects": ["food", "service"],
  "aspect_sentiments": {
    "food": "positive",
    "service": "negative"
  }
}
📈 6. Model Performance
🧪 Training Results
Train Accuracy: 96.7%
Validation Accuracy: 95.9%
📊 Hidden Test Evaluation
Metric	Score
F1 Score	69.5%
Precision	67.9%
Recall	71.1%

🏆 Competition Score:

Pillar 1: 20.85 / 30
📉 7. Performance Analysis
🔹 Strengths
Excellent generalization (small train/validation gap)
Strong handling of:
Arabic text
Franco-Arabic (Arabizi)
Emojis
Robust hybrid system (ML + rules)
🔸 Weaknesses
Moderate F1 score (~69%)
Possible challenges:
Aspect ambiguity
Limited labeled data
Class imbalance
Multi-label complexity
⚙️ 8. System Features
✅ Supports
Arabic text
Franco-Arabic (Arabizi)
Emojis 😊🔥💔
Multi-aspect reviews
🛠️ Handles
Noisy & informal text
Real-world user-generated content
🖥️ 9. User Interface

Built using Gradio

🎯 Features
Input: Review text
Optional: Star rating
Output:
Detected aspects
Sentiment (table format)
📏 10. Evaluation Methodology

Metrics used:

Exact Match Accuracy
Jaccard Similarity
Sentiment Accuracy
F1 / Precision / Recall
💾 11. Model Saving
import joblib
joblib.dump(model, "absa_model.joblib")
