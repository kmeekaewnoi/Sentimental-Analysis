# Sentimental Analysis using Amazon Fine Food Reviews
## Introduction
Sentimental Analysis has been used to analyzed customer opinion in these days. Amazon is one of the biggest online shopping company. Customers usually reviewed their experience after bought the products. The reviews are classifying into 5-star category. The highest score is 5 stars, means customers happy with the product. The lowest score is 1 star, that means customers were not happy with the products. I will use Naive Bayes to make prediction based on customers summary reviews. However, it would be easier to understand the result if we combine some of the reviews  together. Thus, I will combine 1 and 2-star reviews together, and label them as bad reviews. Combine 4 and 5 stars together and label them as good reviews. For 3 stars reviews, I will label them as normal. We will see if the algorithm can make good prediction on the customer reviews.

## Requirement
You will need to install R or RStudio, RStudio can be download at [RStudio](https://www.rstudio.com/products/rstudio/download/).
Also, you will need to install the five following  packages in R.

Packages: "tm", "SnowballC", "wordcloud",  "e1071" , and "gmodels"
## Data
The dataset can be download at [Kaggle](https://www.kaggle.com/snap/amazon-fine-food-reviews) and the dataset is in CSV format.

## Data Explanatory
The data set has 568,454 observations and 10 variables. The variables are ID number, Product ID number, user ID number, customer profile name, helpfulness numerator, helpfulness denominator, customer review in score (1 to 5), time, customer reviews summary in text, and full reviews in text. We are going to use customer reviews summary in text and customer reviews in score only.

  - Look at the proportion of the score.
  
    ![](images/barplot.jpg)
  
  The bar plot above shows the distribution of each review score. We can see that most of customers give 5-star reviews. Four-star reviews are second, and two-star reviews are the least proportion compare to others.

  - Look at some of the customer reviews.
  
  Below are some of the example of the customer summary reviews. 

    "Good Quality Dog Food"
    "Not as Advertised"

  - Look at the customer review after we used the corpus clean up. 
  
    "good quality dog food"

We can see that all the characters are now in lower case.

- Compare the customer reviews after we remove numbers, stop words, punctuation, and eliminate unneeded white space. 
  
  **Before**
  
  "Good Quality Dog Food" 
  
  "Not as Advertised" 
  
  "\"Delight\" says it all" 
  
  **After** 
  
  "good qualiti dog food" 
  
  "advertis" 
  
  "delight say"

  We can see that some of the important words has been removed, and changed the context of the reviews. Such as the word “Not as Advertised” has been transformed into “advertis”, which will change the meaning of the review from negative to be positive.

- Look at the proportion of each score after combined them into 3 categories.
  
  After we combined 4 and 5-star reviews together, we labeled them as “Good”,1 and 2-star are labeled as "Bad, and 3-star reviews are labeled as "Normal". The proportion of each cateory is below. 
  
  Bad       =   0.14894102   ~ 14.9%       
  Good      =   0.76550439   ~ 76.6%        
  Normal    =   0.08555458   ~ 8.5%

 - Wordcloud visualization
  
    The WordCloud below shows the frequent word that customers wrote in the reviews. We can see words that are most used in the reviews are “Great”, “Good”, “Love”,and “Best”.
  
    ![](images/wordcloud1.jpg)

- Wordcloud visualization for " Good " reviews.
  
  The wordcloud below shows the frequent words customer wrote when they gave good reviews. We can see that words that are most used in the reviews are “Great”, “Best”, “Love”, “Delicious”.
  ![](images/wordcloud3.jpg)

- Wordcloud visualization for " Bad " reviews.

    The wordcloud below shows the frequent words customers wrote when they gave bad reviews. We can see words that are most used in the reviews are “Not”,“Bad”, “Awful”, “Horrible”.

    ![](images/wordcloud2.jpg)

## Result
I used the "gmodels" package to give the accuracy.
The tabel below shows the confusion matrix between the actual and predict.

![](images/Matrix1.PNG)

To find the accuracy, we will combine the result from the table start from the left diagonal and divide by all the numbers in the table. 

![](images/result1.PNG)

We get the accuracy = 81%

- Improving model performance
  
We can try to improve the accuracy by using laplace = 1. The confusion matrix shows below.

![](images/Matrix2.PNG)

The accuracy = 82%. By using Laplace, the accuracy only increase by 1 %.

## Conclusion

The Naive Bayes gives an accuracy at most about 82%. The error rate is 18% which is high. This is because there are many words that did not get classified correctly. For example, when customers gave 1-star review with review summary "Not Good", the algorithm divided the review into 2 separate words. And predict it as a positive review because of the word " Good". 

