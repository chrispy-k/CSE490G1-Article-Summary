# CSE490G1-Article-Summary

## Abstract
Everyday we come across abundant amount of texts. From short Twitter posts to news articles, there are so many texts getting generated every day. Manually generating summaries for texts take too much time and effort. Thus, we would like to use deep learning to let the computers do summarization of texts. 

## Video
https://www.youtube.com/watch?v=zbKlvhyU5LE

## Introduction
Recently, I made a habit to read a few articles in the morning to familiarize myself more with what is happening in the world. While I should not always read what I want to read, I sometimes finish an article and feel like I read something else. According to Chartbeat, 92,000 articles get generated each day. Now, if we include things like Twitter posts, Facebook posts, etc, the number is going to be even larger. We definitely cannot read them all, and reading only the ones that interest us will most likely be impossible as well. But, what if we can summarize those articles to few sentences or less? We can definitely manage more texts, and read some other texts that we may never have read because we did not have time.

## Related Work
https://arxiv.org/ftp/arxiv/papers/2108/2108.01064.pdf
I later found this paper and was able to get some insights and what to do in general.

## Approach
I used a Kaggle dataset called "CNN-DailyMail News Text Summarization" : https://www.kaggle.com/gowrishankarp/newspaper-text-summarization-cnn-dailymail. My model first reads the data in. Then, selects only the columns that I am interested in: article and highlight. The model then sees if there is any duplicates in the data or not. This step can may be omitted for others, but I decided to sample 500, 250 and 200 data for train, test and validation because the original dataset is too big (99323, 11449, 13300). From there, model preprocesses the data by getting rid of non-useful words, whitespaces, weird characters. Then, it tokenizes them with pre-trained T5Tokenizer. With that dataset, it then makes Dataloader that will be used for training, testing, and validating. For model, I use pre-trained T5ForConditionalGeneration. To compensate for small batch size, I tried to use gradient accumulation in training function. 

## Results
![image](https://user-images.githubusercontent.com/70288780/145725907-d0707d1a-0e08-4eb3-94d0-8d087b2cc2a9.png)
![image](https://user-images.githubusercontent.com/70288780/145725912-685311fd-8a34-4f58-8dd8-6fb0f0589e62.png)
I evaluated my approach with loss and accuracy. As you can see from the chart, the loss decrease as we go through more epochs, which is nice to see. However, the accuracy fluctuates quite randomly. This is where I think I messed up with the model. I expected the accuracy to increase or be steady. Additionally, we can check how the model is doing by looking at the result that it produces. With the orginal text that starts with "Law-enforcement agencies in South-East Asia...", my model produces "asia grown accustomed breaking records almost every year authorities seized meth drug asia grown". This is understandable, but not quite what we want. It's a bit worse with the original text that starts with "Irving is not eligible to play in home games...". My model produces "barclays center due vaccine mandate new york city could part time player team announced season would allow".

Compared to sentences that got generate from the related work's models, my model's generated sentences are quite bad. This is the paper's T5 model generated sentence: “shopkeeper reported robbery at shopping complex in the morning. he filed a complaint with police and hopes they catch the culprits. the shopkeepers association has issued a notice and asked everyone to stay alert..”. 

## Discussion
From the results, it is apparent that my model needs some work. Some sentences do not quite make sense. I have a few suspicions. First is how I preprocess the data. Right now, I am preprocessing the data so that there is no contractions, stopwords, whitespace, and weird characters. However, to make a sentence understandable, things like comma, period, apostrophe, common stopwords like no, some contractions are needed. Thus, I may need to work on how I preprocess the dataset. Next is how I am predicting and validating my dataset. Currently, I am using loss from the model to predict, but model also gives "logits", which I think what I should use for predicting and validating. However, I was not sure what it represents with the shape of [1, 8, 32128]. Lastly, I later found out from the related work's paper, but there is a way to measure/score NLP models and that is by ROUGE score. Though I was not able to utilize it because I did not have time, but this will definitely help me out when I try to fix the model in the future.

Nonetheless, from this project, I was able to learn many things about NLP and PyTorch. I learned that many ways of filtering/preprocessing to make the data look the way we want them to look. I learned more ways of preparing dataset and utilizing DataLoader. I also learned a new technique, gradient accumulation, for training a model.
