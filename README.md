# Predictive-Analysis-of-Hit-Songs-Using-Repeated-Chorus
In this work, we examined this myth by creating a data set of choruses from popular artists and applied five supervised Machine Learning techniques to predict the popularity purely based on the audio features extracted from a 15s chorus. Using a Neural Network, we were able to demonstrate the performance of the model that is better than random. Hence, we conclude the myth is plausible. Here is the final system design.

![system](https://user-images.githubusercontent.com/68114230/173377223-cd0ff322-fc86-499a-a551-0b5ae7d5b0c4.png)

1. Project Overview 

We created a data set of choruses from popular artists and applied supervised Machine Learning (ML) techniques to predict the popularity of their works purely based on the audio features extracted from the chorus.

2. DATASET 

To the best of our knowledge, there is no publicly available dataset of hooks of songs. Therefore, we have to build the following data pipeline to preparethe data and features.

1.	 Collect the names of popular songs and
      unpopular songs from the same artists the
      from Billboard.com using billboard.py
2.   Download the full songs from Youtube
      using youtube-dl 
3.   Extract the repeated chorus using pychorus
4.   Extract the audio features of the hooks using
      Librosa.

3. CHORUS AND FEATURES

•	3.1 chorus and Audio feature Engineering

With the names of popular artists and their popular and unpopular songs, we fetch the full audio files from Youtube using youtube-dl. For songs with multiple versions, such as remakes or remixes, we choose the first published studio album version. We then use the pychorus to extract 15 seconds of repeated chorus from each song track. The basic idea of pychorus is to extract similar structures from the frequency spectrum. Essentially, it is a form of unsupervised learning and the performance of this extraction is subject to interpretation. But in this
work, we assume they are the ground truth. Empirically, we inspected a few familiar songs and the chorus extracted did match our intuition.

We extracted several audio features from the chorus using librosa. We selected 11 major spectral features for the analysis. Table 1 shows their name, description, and the number of dimensions. The dimensions of the feature set for each track are also a function of ti, where ti is a function of the duration of the chorus (in this case 15s) and the sampling rate of the soundtrack i. Since we do not want the duration or sampling rate to affect the prediction, we transformed the raw dim ensions into 7
Statistic, which are min, mean, median, max, std, skew, kurtosis. In total, each song track produces 518 audio features after the transformation.

•	3.2 The final project dataset

In this dataset, we collected total of 80 unique artists with total of 809 popular and unpopular songs from billboard hit songs on the HOT-100 quarter-end chart between 2006 and 2021. Therefore, the final dataset in this report has a 751 × 518 audio feature matrix and a 751 × 1response vector.

Next, we tried various Feature Engineering and selection techniques like PCA, SELECTKBEST etc. Fine tuned with Some Hyperparameters in the model building section.

Atlast we built an app with streamlit and deployed it to heroku (PAAS). 
Here is the final webapp for the above project. https://songpopularity-checker.herokuapp.com/
