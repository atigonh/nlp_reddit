## Problem Statement ## 
   Contacted by the image-processing team to make a model that will work together with their imaging software in order to enhance the prediction of cats’ and dogs’ images for the incoming Photo caption contest. As data scientists, we'll show them that we not only deal with numbers but we can deal with a text with our secret weapons! (Spoiler alert: It is quite disappointing by the result, the model is quite weak, but some models make a good recall score)

## EXECUTIVE SUMMARY ##
Step 1: Data collections
    Use the example posts from reddit r/cat and r/dog, 5,000 posts for each category, 10,000 in total. Use pushshift to gather the data from reddit, the data is gathered back from Jan 12th, 2023 00:00 to the past until reaches 5,000 posts for each. Then export data to CSV files.
    
Step 2: EDA
    Data comes with several columns, but I am interested in the column that has useful text data for predictions and the column that tells the category. The title column is the only column that has consistent text data and is appropriate for modeling, it contains what people post for their pets. And for the category will use the Subreddit column which tells the exact category name.
    There is no null value for both categories but in Subreddit column there are some data that are not clear for identifying the category cat or dog, so I remove them. Also, remove duplicates title.
    By exploring the title lengths distribution, they are both right-skewed but the dog has a higher average length. And top 5 words after lemmatizing are for cat=(cat, like, love, kitten, cute), for dog=(dog, puppy, breed, help, love). A top emoji is interesting with dog people using paws emoji for their dogs. A sentimental analysis tells that dog people tend to be happier than cat people by 12%.
    After removing unclear category names and duplicates title, both data remain at around 4000, then I mapped cats to '1' and dogs to '0' for machine learning, and exported both categories 4000 each in order to balance the data.

Step 3: Modelling
    For modelling, try out many estimators combine with tokenizers using pipeline and adjust parameters to get the high output using grid search.

## CONCLUSION ##
   Baseline accuracy is 0.5 and all model is better than the baseline, most of them making more than 0.7
   But the model is quite weak, no model reaches 0.8, the best one is stack with models 1,4,7
   AdaBoost is interesting, it make a good recall score of 0.96
   I will pass the stack model and AdaBoost to the image-processing team