# Recommender System 2023 Challenge - Polimi

This repository contains the work done for the [Recommender System 2023 Challenge](https://www.kaggle.com/competitions/recommender-system-2023-challenge-polimi) hosted by Kaggle and reserved for the students of the Recommender Systems course in Politecnico di Milano.

## Competition Overview

The application domain is book recommendation. The datasets provided contain interactions of users with books, in particular, if the user attributed to the book a rating of at least 4. The main goal of the competition is to discover which items (books) a user will interact with.

The datasets include around 600k interactions, 13k users, 22k items (books). The training-test split is done via random holdout, 80% training, 20% test. The goal is to recommend a list of 10 potentially relevant items for each user. MAP@10 is used for evaluation. Any kind of recommender algorithm written in Python can be used.

## Project Overview

The project aims to build a recommender system capable of suggesting items to users based on their past interactions. 

The best performance was achieved through a combination of different strategies:

### Linear Combination Ensembles 

The system uses an ensemble of different recommenders. These recommenders are assembled sequentially, adding one recommender at a time only if it improves the performance. The recommenders are added from the best performing to the least. For more details, please refer to the script `Sequential Ensamble.ipynb`.

### User-Specific Recommender

The recommender system divides the users based on the number of interactions and predicts for each of these groups with a different ensemble. For example, for predicting for users with few interactions, TopPop has a higher weight than others. For more details, please refer to the script `UserSpecific.ipynb`.

### XGBoost

The system leverages XGBoost, using features such as user activity, popularity score, latent features coming from a Deep Encoder, and scores coming from predictions of the most performant ensemble. For more details, please refer to the script `XGBoost.ipynb`.

## Data Preprocessing

The data preprocessing phase involved several steps to enhance the performance of the recommenders. Cold users and items were removed from the User-Item Interaction Matrix (URM) to reduce noise and improve the accuracy of the recommendations. A mapping was implemented to revert to the original user and item IDs for submission. The existing class was modified to automatically manage the presence of cold users and items and preprocessed URMs. The implementation can be found in 'Data Preprocessing.ipynb'.

## Wrappers

A wrapper for `LinearCombinationEnsemble` was created from scratch to automate the training and inference for recommenders built of different ones. This wrapper exploits the ability of the ensemble to combine the strengths of multiple recommenders and mitigate their weaknesses, leading to more accurate and diverse recommendations.

Analogously the 'UserSpecific' class was implemented, making the use of a combination of Recommenders specific to the user, based on its profile length, more intuitive.

See 'Recommenders' folder for a deeper insight.

## Results

The combination of these strategies resulted in a robust and performant recommender system, achieving high scores in the competition.

