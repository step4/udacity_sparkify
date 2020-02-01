
# udacity_sparkify
 Capstone Project of the DataScientist Nanodegree
___

This repository contains the jupyter notebook, and a version of the completed notebook as html, used to solve the capstone project of the DataScientist Nanodegree.

In this project you will face event data of a music streaming service called *sparkify*. The event data contain events of users, which interact with sites like *NextSong*, *Add to Playlist* etc.

The task was to handle a large and realistic dataset with Spark to predict the user's churn. 
So the steps were:

 - Read a 12GB large dataset
 - Removal of unnecessary and missing data
 - Execution of a Exploratory Data Analysis
 - Development and engineering of features
 - Training and Validation of a classification model 
 
A detailed write up can be found at [Music and people — hand in hand for centuries.](https://medium.com/@c.rausch020/music-and-people-hand-in-hand-for-centuries-a253af2378fc)

___
## Files

 - [sparkify-nb.ipynb](https://github.com/step4/udacity_sparkify/blob/master/sparkify-nb.ipynb "sparkify-nb.ipynb") - the actual notebook which was executed on a AWS EMR Cluster
 - [sparkify-nb.html](https://github.com/step4/udacity_sparkify/blob/master/sparkify-nb.html "sparkify-nb.html") - a html export to summerize the execution of the notebook
 - [img - directory](https://github.com/step4/udacity_sparkify/tree/master/img) this directory contains all images used in the blogpost on medium and in this readme 

___
## How to run
To run this notebook without any changes you need a AWS account.

 1. Login to your AWS console at [https://aws.amazon.com/](https://aws.amazon.com/)
 2. Choose the Analytics service EMR (Elastic Map Reduce)
 3. Press on *Create Cluster*
 4. Choose an arbitray name like *sparkify-cluster*
 5. Choose atleast the release `emr-5.29.0` and the applications `Spark: Spark 2.4.4 on Hadoop 2.8.5 YARN with Ganglia 3.7.2 and Zeppelin 0.8.2`
 6. Choose the instance type `m3.2xlarge` or `r4.2xlarge` if you need a faster calculation
 7. Choose as EC2 key pair `Proceed without an EC2 key pair`
 
**Have in mind that the cluster costs between 0.50$ and 1.50$ per hour. So terminate the cluster if you don't need it**

When the cluster is ready create a jupyter notebook at the EMR settings and use the code from this repository.
___
## Results of analysis
Overall the notebook used `matplotlib` and `seaborn` for plotting bar charts, boxplots and confusion matrices. To get the input values for the plots, the data was collected and converted to a pandas dataframe.
`sklearn` was used to generate the confusion matrices.

All other steps like reading, cleaning, EDA, feature engineering, modelling etc. were done with Spark, respectively `pyspark`.

Out of the 12GB of event data the training data contains 22278 rows for each userId and 16 columns for each feature.
The trained models are binary classifiers for churn or not churn.

Without parameter tuning Logistic Regression, Random Forest and Gradient Boosted Trees were trained. The GBT classifier had the best accuracy of 0.866 and f1-score of 0.860. So only GBT was used for a Cross Validation.

After parameter tuning the GBT model got an accuracy of 0.868 and a f1-score of 0.858.
The model improved a tiny bit in regard to the accuracy but lost a bit in the f1-score.

The confusion matrix is:
![Confusion Matrix Tuned GBT Model](https://github.com/step4/udacity_sparkify/blob/master/img/gbt_cv_conf.PNG?raw=true)

Nevertheless it was possible to predict around 310 true possitives in the validation set.

___
## Possible Improvements

One improvement could be the extension of the hardware limitations of the EMR cluster. With more powerfull nodes it is possible to train the GBT classifier with a much broader parameter grid to find a better hyperparamter set for this problem.

Moreover one could look into more different features extracted from the event data. For example a more detailed exploration of the location data could give good indicators for churn.

___
## Conclusion

It was a very interesting digging into the field of Big Data. The date set contained only event data of users interacting with the platform. Exploring and analysing this data to conclude on features which hopefully seem to be useful was a motivational and informative task.

In addition the usage of a cloud based cluster solution like AWS EMR reduced the fear of contact which these services. So I will probably use them much more often for other projects.