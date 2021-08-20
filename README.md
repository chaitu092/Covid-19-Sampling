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


[References]
