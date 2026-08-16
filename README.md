# Financial Sentiment Analysis Journal

## What this repo is about

Have you ever wondered how machines can read financial news and instantly know if it's good or bad news for a company? That's exactly what this project is all about. The goal of this repository is to build a machine learning model that can read financial sentences and classify their sentiment into three categories: **Negative (0)**, **Neutral (1)**, and **Positive (2)**.

To achieve this, I used the **Financial PhraseBank** dataset, a collection of financial news sentences labeled by experts. The challenge was to see how well different techniques, from traditional machine learning to state-of-the-art deep learning, could understand the complex and specific language used in finance.

## What I did

My journey to solve this problem happened in three main chapters:

**Chapter 1: The Traditional Approach**
I started with the basics of Natural Language Processing (NLP). I cleaned up the text by making everything lowercase and removing punctuation. Then, I used a **Word2Vec** model to turn words into 100-dimensional vectors, averaging them to represent entire sentences. With these features, I built an ensemble **Stacking Classifier** combining **XGBoost** and **Random Forest**, with a Logistic Regression meta-learner. It was a solid start, but the accuracy hovered around **60.25%**. It was great at identifying 'Neutral' sentences but struggled with the nuances of 'Positive' and 'Negative' financial jargon.

**Chapter 2: Pushing the Limits**
I refused to give up on my traditional models just yet. I spent time optimizing the XGBoost model using **GridSearchCV** to find the perfect learning rate and depth, and I explored Cost Complexity Pruning for the decision trees. This hard work paid off slightly, pushing the accuracy up to **64.72%**. However, I realized I had hit a wall. The simple Word2Vec approach just couldn't capture the deep context of the sentences.

**Chapter 3: The Deep Learning Breakthrough**
Knowing I needed a model that truly understood financial context, I brought in the heavy artillery: **FinBERT**. FinBERT is a transformer-based model pre-trained specifically on financial text. Instead of training embeddings from scratch, I used the Hugging Face `transformers` pipeline to leverage FinBERT's immense pre-existing knowledge.

## What's the result

The results were nothing short of amazing! When I unleashed FinBERT on the dataset, the performance skyrocketed.

I achieved an **86.94% accuracy** on the validation set and a final **89.69% accuracy** on the unseen test data.

**Why was FinBERT the ultimate winner?**
1. **Context is King:** Unlike my earlier Word2Vec model, which assigned a fixed vector to a word regardless of where it appeared, FinBERT reads the whole sentence and understands how surrounding words change meaning.
2. **Speaks the Language:** Because FinBERT was trained specifically on financial documents, it already knew that words like "loss" or "EBITDA" carry specific weight in the financial world.
3. **Balanced Predictions:** It finally managed to accurately predict the harder-to-catch 'Positive' and 'Negative' sentiments, overcoming the imbalance issues my earlier models faced.

In the end, this project taught me a valuable lesson: while traditional machine learning ensembles are great and resource-efficient, when it comes to understanding complex domain-specific language, Transformer models like FinBERT are absolute game-changers.
