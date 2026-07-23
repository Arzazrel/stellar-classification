# ProjectDM22, Project of Data Mining, year 2022

## Overview

Folder of the Astreo application, a machine learning application built in Python for the Data Mining and Machine Learning project (Master's in AI and Data Engineering, University of Pisa).

**Astreo** is a machine learning application that classifies celestial bodies (galaxy / star / quasar) from their spectral data, aimed at amateur astronomers. 

**Goal & guiding constraint**: 
The distinguishing design choice is accessibility: the classifier is meant to work with data that a hobbyist can realistically obtain at home, using consumer-grade telescopes and filters. 
This constraint deliberately shaped the feature selection. 
In particular, I excluded the redshift feature — even though analysis showed it was the single strongest predictor of the class — because measuring redshift requires elaborate techniques and equipment unavailable to amateurs. 
The model therefore relies only on positional (α, δ) and photometric ugriz features, plus removal of instrument-related features (telescope/plate/observation IDs) that carry no physical meaning about the object.

**Methodology**: 
Full data-mining pipeline: data cleaning, feature reduction, per-algorithm transformations (z-score normalization for K-NN, Fayyad-Irani supervised discretization for Naive Bayes). 
Several classifiers were compared under 10-fold cross-validation (J48/C4.5, JRIP, Naive Bayes, K-NN, and ensembles: Bagging, AdaBoost, Random Forest) across multiple attribute-selection strategies, with dataset-rebalancing experiments (SMOTE). 
Model selection was confirmed with paired t-tests for statistical significance.

**Result**: 
Random Forest was selected — statistically the best — reaching ~88% average accuracy using only amateur-obtainable features.

**Possible future work** 
Since redshift was the most informative feature but is inaccessible to amateurs, a natural extension is a two-stage model: first estimate the redshift from the same photometric ugriz data (photometric redshift estimation is itself a studied ML problem), then feed the predicted redshift into the classifier to boost accuracy. 
The net benefit is not guaranteed — the estimation error propagates downstream — so it would need to be validated empirically, but it is a promising direction for closing the accuracy gap without requiring specialized hardware from the user.

**Tech stack**: 
Python (scikit-learn, Tkinter GUI), Weka (model evaluation), MySQLWorkbench V6.1 and MySQL server V 5.6

## Dataset
The dataset used for the application can be found on kaggle at the following link: https://www.kaggle.com/fedesoriano/stellar-classification-dataset-sdss17
Release 17 of the Sloan Digital Sky Survey (SDSS), ~100k observations.

## Hardware used

CPU: Intel(R) Core(TM) i7-10870H CPU @ 2.20GHz 2.21 GHz RAM: 16 GB GPU: RTX 3060 6GB laptop

## The folder contains:
- 3 python files: AstreoGUI (main file, GUI), Classifier, DB_connect
- dataset folder: contains the dataset in csv format
- Dump_DM_project_DB: MySQL database
- Others folder: for future implementations or machine learning experiments in Python
- Data_Mining_Documentation: documentation regarding the application and the analysis carried out for the choice of model and parameters.

## Procedure for use:
1) import the DB into MySQL Workbench
2) start mysql server
3) run 'AstreoGUI' file

Below there is a list of celestial bodies that can be used to test the application classifier. 
If you wish to use them:
- open the application, log in or sign in, press the "Add celestial bodies" button
- enter the data given for each object in the corresponding fields on the screen 
- press "classify 
- compare the actual class with the one visualised in the application

OBJECT IN DB
1)
ra	135.6891066036
dec	32.4946318397087
type	"GALAXY"
u	23.87882
g	22.2753
r	20.39501
i	19.16573
z	18.79371

2)
ra	340.995120509191
dec	20.5894762801019
type	"QSO"
u	23.48827
g	23.33776
r	21.32195
i	20.25615
z	19.54544

3)
ra	44.3740887871866
dec	3.01793310249287
type	"GALAXY"
u	25.76758
g	22.40062
r	20.49454
i	19.55738
z	19.04092

4)
ra	182.941369205209
dec	54.4456260755977
type	"STAR"
u	22.25055
g	20.72246
r	20.20829
i	19.9893
z	19.95151

5)
ra	340.995120509191
dec	20.5894762801019
type	"QSO"
u	23.48827
g	23.33776
r	21.32195
i	20.25615
z	19.54544

OBJECT NOT IN ORIGINAL DB BUT ADDED BY USER: 'alex'
1)
ra	187.35052
dec	2.13672
type	GALAXY
u	19.18
g	18.02
r	17.42
i	17.05
z	16.89

2)
ra	187.37097
dec	2.17290
type	STAR
u	14.77
g	14.47
r	14.77
i	12.70
z	13.06

3)
ra	187.40927
dec	2.20450
type	STAR
u	21.04
g	18.07
r	16.61
i	15.11
z	14.30

OBJECT NOT IN DB
1)
ra	229.56651
dec	42.72935
type	STAR
u	15.06
g	15.19
r	13.75
i	13.78
z	13.60

2)
ra	229.52653
dec	42.74407
type	GALAXY
u	17.44
g	15.81
r	15.20
i	14.91
z	14.57

3)
ra	229.53922
dec	42.74627
type	STAR
u	19.19
g	16.56
r	15.19
i	14.14
z	13.61

4)
ra	228.39238
dec	41.95874
type	GALAXY
u	15.36
g	13.95
r	13.26
i	12.91
z	12.67

5)
ra	187.27792
dec	2.05239
type	QSO
u	13.99
g	13.00
r	12.89
i	12.64
z	13.24

## Developer's notes:
	The work related to the university examination is finished and the project is completed. 
	There may be updates or improvements to the project in the future.

## Developers:
	- Alessandro Diana