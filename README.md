# Positive Tweet Sentiment Classification Model.
**Created by Lucas Fishbein**

<div>
<img src="https://github.com/LucasFishbein/Positive_Tweet_Sentiment_CNN_Model/assets/117129342/0fa04819-2431-431f-96de-15a66cd69a67" width="500">
</div>

# Getting Started with this Repository



# Overview and Business Problem


With so many consumers taking to social media sites to express their opinions on brands and products, it can be very hard as a company to pull useful information from the tsunami of messages that may be directed at a company or product. The current project aims to help companies make use of the information locked in these tweets by building a classification model that will allow companies to input the text of a tweet, or many tweets at once, and automatically classify the sentiment of that tweet as being "Positive" or "Not positive".  This will allow for a company to better organize and make use of the information provided in the tweets they receive after unveiling a new product or just in general.

A classification model of this style can provide many uses, a few simple examples of the possible uses are:

1. Being able to gauge the public opinion on a product/brand/service
2. Make use of direct unfiltered feedback from the consumers
3. Model can be easily retrained on a custom dataset to more closely target specific products, locations or other focuses.
4. Identify those who already have shown postive/negative interest in the product.
    > 4a. Better understand target demographics\
    > 4b. Advertise directly to those who already like your product\
    > 4c. Use social media to advertise to the peer circles of people who like the product

# Tweet Sentiment Classification Model's Performance

A Binary Classification NLP Model was built out using a sequential convolutional neural network, after many iterations, the final model and was able to classify the sentiment of a set of novel tweets correctly as either "Positive" or "Not Positive" 76% of the time, this is significantly better than random chance and can provide a variety of useful information about those tweets and the users who sent them. 

## Model's Performance on Classifying Positive Tweet

As can be seen via the confusion matrix below, the model performs significantly better on "Not Positive" tweets and this is supported by the "Not Positive" set having an F1 score of 0.84 while the "Positive" tweets have an F1 score of 0.57. The loss for the test group was at an acceptable level of 0.63.

<img width="652" alt="Screenshot 2023-06-12 at 4 57 09 PM" src="https://github.com/LucasFishbein/Positive_Tweet_Sentiment_CNN_Model/assets/117129342/508d0a40-eda4-4772-9b26-8fdfb2858707">
    
 precision    recall  f1-score   support

**Not Positive**   0.80      0.88      0.84       614
**Positive**       0.65      0.51      0.57       278

    accuracy                           0.76       892
   macro avg       0.72      0.69      0.70       892
weighted avg       0.75      0.76      0.75       892
    
# Database Understanding

The Present dataset contains a series of 9093 Tweets pre-labeled by human raters. Raters judged if the tweet's text expressed a positive, negative or no emotion towards a brand and/or product, any time an emotion was expressed, the rater was then asked to identify the brand or product that was the target of that emotion. 

The Tweets were in large part centered on Apple and Google products during/after the 2011 South by Southwest (SXSW) Conference. The resulting datafile contains three columns per row, one for the tweet's text, one for the emotion expressed and one for the target product/brand of that emotion, when identifiable. 

Data was sourced from CrowdFlower via [data.world](https://data.world/crowdflower/brands-and-product-emotions), added by Kent Cavender-Bares on August 30, 2013.


# Data Cleaning and Preprocessing

The text of every tweet was cleaned of extraneous characters such as punctuation, urls, hashtags and typical stopwords. This cleaning was followed by tokenization and then the lemmatization of these tokens so that the resulting text was a list of lemmatized words seperated as tokens for each tweet.

The data was then split into training, testing and validation groups at a ratio of 8:1:1

The tokenized tweets and labels were then padded and converted into arrays for input into the CNN model.


# Exploratory Data Analysis 

As can be seen in the graph below, the data's classes were unbalanced at a ratio of about 2:1, "Not Positive" to "Positive".

<img width="615" alt="Screenshot 2023-06-12 at 7 38 24 PM" src="https://github.com/LucasFishbein/Positive_Tweet_Sentiment_CNN_Model/assets/117129342/9dfd8fc0-8b80-41a3-9266-ea58c529983b">

## Engineered Fetures

A number of features were engineered and explored for trends, the features include; Brand tweet is directed at, number of words per tweet, and the tweet hashtags were pulled out.

While the extra features would be useful in providing information to a brand trying to extract information from tweets after they were labeled by this model, no obvious trends could be found within these engineered features and in the end they were not included in the model. 

<img width="590" alt="Screenshot 2023-06-12 at 8 43 25 PM" src="https://github.com/LucasFishbein/Positive_Tweet_Sentiment_CNN_Model/assets/117129342/f381647f-73bf-4ea5-9608-0fa8ab3c45dc">

## N-Grams 

N-Grams of various sizes were explored by sentiment label, unfortunately for the present dataset, this information was not useful in modeling as the top phrases were very consistent across sentiment labels as seen below.

<img width="586" alt="Screenshot 2023-06-12 at 8 52 37 PM" src="https://github.com/LucasFishbein/Positive_Tweet_Sentiment_CNN_Model/assets/117129342/7d5f7e54-ed7c-45f3-a592-63ac12b21e8d">


# Modeling

Modeling started off with a fairly basic sequential CNN model that contained 3 dense layers and was compiled for accuracy via the "adam' optimizer and used binary crossentropy as the loss metric.

Models were trained via the training set and the validation st as the validation data. The model was fit and then examined for accuracy and loss across training epochs. The test set of data is then run through the model and evaluated via confusion matrices and classification reports.

The baseline model was iterated on in order to improve the overall performance, with such additions as dropout layers and regularization techniques to limit overfitting but after 4 iterations this model's philosphy was not working as expected and a new model was designed under the name "Model B".

Model B is another sequential CNN but this model made use of an Embedding layer as well as LSTM and GlobalMaxPool1D layers in addition to three dense layers. The baseline model was again very overfit, to mend this issue dropout layers and L2 regularization was added. After a number of iterations in which the model's hyperparameters were tuned in an attempt to increase accuracy and limit overfitting, a final model was choosen by comparing all of the models that were built.


# Final Model for Positive Tweet Sentiment Classification

 <img width="652" alt="Screenshot 2023-06-12 at 4 57 09 PM" src="https://github.com/LucasFishbein/Positive_Tweet_Sentiment_CNN_Model/assets/117129342/508d0a40-eda4-4772-9b26-8fdfb2858707">
    
    

                precision    recall  f1-score   support

**Not Positive**   0.80      0.88      0.84       614
**Positive**       0.65      0.51      0.57       278

    accuracy                           0.76       892
   macro avg       0.72      0.69      0.70       892
weighted avg       0.75      0.76      0.75       892



# Conclusions and Practical Implementations

A

# For More Information
See the full analysis in the [Jupyter Notebook]() 

For additional info, contact Lucas Fishbein at FishbeinLucas@gmail.com

## Repository Structure

```
├── .gitignore
├── CONTRIBUTING.md
├── .ipynb
├── data
├── LICENSE.md
└── README.md
```

