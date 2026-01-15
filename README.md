# SmartCatalogAI: Semantic Pricing Engine for Retail Catalogs
Predicting retail prices from product descriptions is underdetermined because pricing depends not only on intrinsic product attributes but also on competitive context and category positioning. SmartCatalogAI addresses this by combining semantic embeddings, unsupervised clustering, and regression models to estimate product prices using only catalog text.

# Project Overview
This project builds a semantic pricing model for ~75,000 retail products using only textual descriptions. The approach integrates:
i) Representation Learning — to capture product semantics
ii) Latent Taxonomy Discovery — to reveal competitive peer groups
iii) Pricing Priors — to incorporate category market structure
iv) Supervised Regression — to estimate retail price levels
The final system demonstrates that price formation depends jointly on semantic attributes and market-level priors.

# Problem Statement
Given a product’s textual description, estimate its market price without additional product attributes such as brand, rating, or category labels.

# Dataset
~75,000 product listings
Fields used:
description (text)
price (numeric target)
No explicit category labels or metadata were provided.

# Methodology
## Baseline Experiments
### Embedding Models Tested:-
TF-IDF (sparse lexical) 
FastText (subword embeddings)
SentenceTransformers (semantic sentence vectors)
### Regressors Evaluated:-
XGBoost
LightGBM
CatBoost
### Baseline performance:
SMAPE = 58

# Semantic Feature Engineering
To capture category structure:
(1) Category Induction (Latent Taxonomy)
Used bert-base-nli-mean-tokens embeddings for product semantics
Applied KMeans clustering on embeddings → 121 latent product categories
These clusters approximate product types (e.g., tea, jeans, speakers, kettles, etc.)
Added as new categorical feature.

(2) Category Pricing Prior
Computed mean cluster-level prices:
Added as new numeric feature:

These two features model competitive pricing anchors.

# Final Pricing Model
Embedding: bert-base-nli-mean-tokens
Features:
-> Semantic embeddings
-> Automated_Category_ID
-> Mean_Category_Price
Regressor: XGBoost

# Tech Stack
## NLP / Embeddings
Sentence-BERT (bert-base-nli-mean-tokens)
FastText
TF-IDF
## ML / Modeling
XGBoost
LightGBM
CatBoost
## Clustering
KMeans
## Metrics
SMAPE
                                        n
                            100/n   X   ∑   2|y true  -  y pred|/|y true| + |y pred|
                                        i=1
