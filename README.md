# CSE490G1-Article-Summary

## Abstract
Everyday we come across abundant amount of texts. From short Twitter posts to news articles, there are so many texts getting generated every day. Manually generating summaries for texts take too much time and effort. Thus, we would like to use deep learning to let the computers do summarization of texts. 

## Video
To be added

## Introduction
Recently, I made a habit to read a few articles in the morning to familiarize myself more with what is happening in the world. While I should not always read what I want to read, I sometimes finish an article and feel like I read something else. According to Chartbeat, 92,000 articles get generated each day. Now, if we include things like Twitter posts, Facebook posts, etc, the number is going to be even larger. We definitely cannot read them all, and reading only the ones that interest us will most likely be impossible as well. But, what if we can summarize those articles to few sentences or less? We can definitely manage more texts, and read some other texts that we may never have read because we did not have time.

## Related Work
https://arxiv.org/ftp/arxiv/papers/2108/2108.01064.pdf
I was able to get some insights and general idea of what to do from this paper

## Approach
I used a Kaggle dataset called "CNN-DailyMail News Text Summarization" : https://www.kaggle.com/gowrishankarp/newspaper-text-summarization-cnn-dailymail. My model first reads the data in. Then, selects only the columns that I am interested in: article and highlight. The model then sees if there is any duplicates in the data or not. This step can may be omitted for others, but I decided to sample 500, 250 and 200 data for train, test and validation because the original dataset is too big (99323, 11449, 13300). From there, model preprocesses the data by getting rid of non-useful words, whitespaces, weird characters. Then, it tokenizes them with pre-trained T5Tokenizer. With that dataset, it then makes Dataloader that will be used for training, testing, and validating. For model, we use pre-trained T5ForConditionalGeneration. 

## Results
![image](https://user-images.githubusercontent.com/70288780/145725907-d0707d1a-0e08-4eb3-94d0-8d087b2cc2a9.png)
![image](https://user-images.githubusercontent.com/70288780/145725912-685311fd-8a34-4f58-8dd8-6fb0f0589e62.png)


## Discussion

You can talk about your results and the stuff you've learned here if you want. Or discuss other things. Really whatever you want, it's your project.
