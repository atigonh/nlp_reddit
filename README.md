## Problem Statement ## 
   Contacted by the image-processing team to make a model that will work together with their imaging software in order to enhance the prediction of cats’ and dogs’ images and text classifications for the incoming Photo caption contest. As data scientists, we'll show them that we not only deal with numbers but we can deal with a text with our secret weapons' NLP! (Spoiler alert: It is may disappointing by the result, the score not much sastified, but some model make a good recall score)

## EXECUTIVE SUMMARY ##

## STEP ##
Step 1: Data collections
    Use the example posts from reddit r/cats and r/dogs about 6_000 posts for each category, 12_000 in total. Use pushshift to gather the data from reddit, the data is gathered back from Jan 12th, 2023 00:00 to the past until reaches around 6_000 posts for each. Then export data to CSV files.
    
Step 2: EDA
    Data comes with several columns, but I am interested in the column that has useful text data for predictions and the column that tells the category. The 'title' column is the only column that has consistent text data and is appropriate for modeling, it contains what people post for their pets. And for the category will use the 'subreddit' column which tells the exact category name.
    There is no null value for both categories but in subreddit column there are some data that are not clear for identifying the category cats or dogs, so I remove them. Also, remove duplicates title.
    By exploring the title lengths distribution, they are both right-skewed but the cats has a higher average length. And top 5 words after stemming are for cat=(cat, like, love, just, kitten), for dog=(dog, help, puppi, advic, need). Emoji analysis is interesting, cats people using emoji more than dogs people a lot like 20 times. A sentimental analysis tells that cats are happier than dogs people by 6 times.
    After removing unclear category names and duplicates title, both data remain at around 5_700-5_900, then I mapped cats to '1', and dogs to '0' for target category, and concatenate both categories by 5_000 each in order to balance the data, total rows will be 10_000.

Step 3: Modelling
    For modelling, try out many estimators combine with various tokenizers using pipeline and adjust parameters to get the highest output using grid search.

## CONCLUSION ##
   Baseline accuracy is 0.5 and all model is better than the baseline, some of them reach score by 0.9
   **The best model is Stack model which is combine 3 models: model 1, 4, 7 and get the test score around 0.93 and f1 score 0.93 as well.**
   Best recall score is from model 8 with recall score 0.98
   Best sensitivity score is from model 7 with sensitivity score 0.93
   
   I will pass the stack model and both best recall/sensitivity models to the image-processing team with explanation

## RECOMMENDATION ##
   In order to improve the model, we should gather bigger dataset, or use/add another source of data, and using new word remove/token techniques.