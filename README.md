🚀 Project Overview
The goal of this project is to perform multi-class emotion classification on text data, specifically from chat logs. Recognizing emotions like joy, sadness, anger, fear and surprise, in a conversational context is a challenging NLP task.

To achieve robust performance, this project does not rely on a single model. Instead, it uses a stacking ensemble to learn from the predictions of three different base models:

BiLSTM: A classic recurrent neural network that excels at capturing sequential patterns and context from both directions in a sentence.

DistilBERT: A lighter, faster, and distilled version of BERT that retains most of its performance, making it excellent for efficient fine-tuning.

RoBERTa: A robustly optimized version of BERT that often achieves state-of-the-art results on NLP tasks.

The final prediction is made by a "meta-model" that learns the optimal way to combine the outputs of these three base models.

🤖 Model Architecture
The model is built using a two-level stacking approach.

Level 0: Base Models
Three independent models are trained to predict emotion probabilities from the input text:

BiLSTM Model:

Embedding Layer (GloVe)
Bidirectional LSTM Layer
Global Max Pooling Layer
Dense Output Layer (with softmax)

DistilBERT Model:

distilbert-base-uncased (fine-tuned)
Dense Output Layer (with softmax)

RoBERTa Model:
roberta-base (fine-tuned)
Dense Output Layer (with softmax)

Level 1: Meta-Model (Stacker)
The predictions (probability distributions) from the three Level 0 models are concatenated to form a new feature vector. This vector is then used to train a simpler "meta-model."
Input Features: [BiLSTM_prob_1, ..., BiLSTM_prob_N] + [DistilBERT_prob_1, ..., DistilBERT_prob_N] + [RoBERTa_prob_1, ..., RoBERTa_prob_N]
Meta-Model: A Logistic Regression model (or a simple shallow Neural Network) is trained on these new features to produce the final, ensembled emotion classification.


✨ Features
Multi-Class Classification: Categorizes chat text into 6 emotion classes.

Hybrid Approach: Combines classic RNNs and modern Transformers.

High Accuracy: Leverages stacking to achieve better performance than any single model.

Separate Preprocessing: Includes distinct tokenization pipelines for word-based (BiLSTM) and sub-word-based (Transformer) models.
