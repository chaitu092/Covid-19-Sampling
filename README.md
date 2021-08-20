# Covid-19-Sampling

## Objective
1. Predict confirmed COVID-19 cases among suspected cases.
Based on the results of laboratory tests commonly collected for a suspected COVID-19 case during a visit to the emergency room, would it be possible to predict the test result for SARS-Cov-2 (positive/negative)?

2. Based on the results of laboratory tests commonly collected among confirmed COVID-19 cases during a visit to the emergency room, would it be possible to predict which patients will need to be admitted to a general ward, semi-intensive unit or intensive care unit?

## Dataset
This dataset contains anonymized data from patients seen at the Hospital Israelita Albert Einstein, at São Paulo, Brazil, and who had samples collected to perform the SARS-CoV-2 RT-PCR and additional laboratory tests during a visit to the hospital.

All data were anonymized following the best international practices and recommendations. All clinical data were standardized to have a mean of zero and a unit standard deviation.

## EDA and Class Imbalance
![image](https://user-images.githubusercontent.com/46320744/130268877-99b3f4d6-9e70-4d4a-9030-f2d8f0c7604f.png)

![image](https://user-images.githubusercontent.com/46320744/130269276-36c4d566-4643-4828-b05c-f8503401a9dc.png)

## Modeling
I tried several strategies to handle the class imbalance problem (having 603 observations and only 83 positivess), but the one that actually worked and improved the recall of my model was somewhat non-traditional: I created two separate dataframes, Covid-positives and negatives, shuffled the rows of the Covid-negatives dataframe, cropped it to match the dimension of the positive dataframe (83, 36), concatenated them and shuffled again. Also applied several sampling techniques named, 
1. Random Undersampling
2. Random Oversampling
3. Shuffling Undersampling
4. SMOTE
5. TOMEK
6. ADASYN
7. SMOTETomek
Surprisingly, using the built-in method for random undersampling didn't result in improvement of the recall or accuracy score.

My final model, that performed the best, was XGBoost with  random oversampling. I was able to spot the positives with 97.31% accuracy.


## [References]

1.https://arxiv.org/abs/1106.1813

2.https://medium.com/@411.codebrain/train-test-split-vs-stratifiedshufflesplit-374c3dbdcc36#:~:text=During%20data%20splitting%20operations%2C%20train_test_split,while%20StratifiedShuffleSplit%20represents%20Stratified%20Sampling.&text=In%20will%20be%20using%20the,notebook%20can%20be%20found%20HERE.

3.https://medium.com/dataman-in-ai/sampling-techniques-for-extremely-imbalanced-data-part-i-under-sampling-a8dbc3d8d6d8
4.https://analyticsindiamag.com/correcting-class-imbalanced-data-for-binary-classification-problems-demonstrations-using-animated-videos/
5.https://towardsdatascience.com/class-imbalance-problem-in-classification-a2ddaba98f4a
