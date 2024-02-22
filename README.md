# Recommender System 2023 Challenge - Polimi

This repository contains the work done for the [Recommender System 2023 Challenge](https://www.kaggle.com/competitions/recommender-system-2023-challenge-polimi) hosted by Kaggle and reserved for the students of the Recommender Systems course in Politecnico di Milano.

## Competition Overview

The application domain is book recommendation. The datasets provided contain interactions of users with books, in particular, if the user attributed to the book a rating of at least 4. The main goal of the competition is to discover which items (books) a user will interact with.

The datasets include around 600k interactions, 13k users, 22k items (books). The training-test split is done via random holdout, 80% training, 20% test. The goal is to recommend a list of 10 potentially relevant items for each user. MAP@10 is used for evaluation. Any kind of recommender algorithm written in Python can be used.

## Project Overview

The project aims to build a recommender system capable of suggesting items to users based on their past interactions. The best performance was achieved through a combination of different strategies:

### Ensembles of Different Recommenders

The system uses an ensemble of different recommenders. These recommenders are assembled sequentially, adding one recommender at a time only if it improves the performance. The recommenders are added from the best performing to the least. For more details, please refer to the script `Sequential Ensamble.ipynb`.

### User-Specific Recommender

The recommender system divides the users based on the number of interactions and predicts for each of these groups with a different ensemble. For example, for predicting for users with few interactions, TopPop has a higher weight than others.

### XGBoost

The system leverages XGBoost, using features such as user activity, popularity score, latent features coming from a Deep Encoder, and scores coming from predictions of the most performant ensemble.

## Results

The combination of these strategies resulted in a robust and performant recommender system, achieving high scores in the competition.

