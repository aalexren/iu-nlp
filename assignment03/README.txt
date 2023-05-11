# Assignment 3 Report

Team members:
- Sergey Golubev
- Andrey Vagin
- Artem Chernitsa

Our submission consists of two files: bert.ipynb and models.ipynb.

At first, we tried to use the article (https://towardsdatascience.com/named-entity-recognition-with-bert-in-pytorch-a454405e0b6a) 
suggested in the competition description.
The results of this work can be found in bert.ipynb file. 

We wrote several methods to convert NEREL dataset format into needed for BERT training.
While training process we faced a problem that we were not able to solve.
Labels for the training have the following format:
'Марио Монти подаст в отставку' -> 'B-PERSON I-PERSON O O O'

After several steps of training our model always had been starting to predict only 'O' tags
for all the tokens which gave accuracy of 0.749 (ratio of tokens without named entities) and zero F1 score.
We tried several methods to solve this issue. First of all, tokenizer used in the article
was from the other model, so we changed it to the right one. Then we tried different optimizers,
learning rates for them, batch size. We tried to debug the model behaviour line by line but
the result was always the same: model started to predict 'O' for all tokens.

Then we decided to try other models for our task. In models.ipynb you can find the result of
tirals wth other models.

Firstly, we tried Natasha library. It has pretrained model for NER but it supports only 3 different tags out of
29 needed ones. Our only submission was obtained with this model.

Secondly, we tried DeepPavlov. It did not work well out of box as big part of our tokens are very specific.
Trials to fine-tune the model failed.

The last and the worst model that we tried was Spacy. It recognizes very few number of tokens.

P.S. One of the possible solutions may be the usage of one these models:
https://github.com/nerel-ds/nested-ner-benchmarks
