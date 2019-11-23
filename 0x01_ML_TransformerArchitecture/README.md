# The Transformer Architecture

## Basics

The basic building blocks (layers) of the transformer architecture are:

* Embedding the input and output vocabulary
* Positional encodings
* Masking
* Attention
* Feed-Forward-Networks
* Normalization

### Embedding the input and output vocabulary

If you are going to implement a machine translation system, you may have two languages involved, the source language (e.g. english) and the destination language (e.g. german).
Both of them have a different vocabulary and also have different embeddings.  

But there are also valid configurations, where the source and the destination language are the same. 
Like when you want to predict the next words of an english input.
Then you use the same vocabulary as your input and output vocabulary and the same embeddings. 

Thus we can have different embeddings depending on the input and the output languages, when they differ and same embeddings, when the input and output language are the same.

* BPE statistics and BPE vocabulary is used to guide the encoder, which byte/symbol/character pairings to prefer over others. 
  That will lead to the "same" meaning and deterministic encoding.
  
* Given these rules (bpe-statistics, bpe-vocabulary), we now encode the whole corpus and calculate the optimal representation with the Word2Vec algorithm, which optimizes the
  prediction of the next word or subword. 
  
* Embedding gives some very interesting results, the famous example is: The closest vector of ('king' - 'man' + 'woman') is 'queen'. 
  The vector space contains some very interesting properties, like you can calculate vectors for fast -> faster -> fastest and apply these 
  vectors for the word slow, then you will calculate the words "slower" and "slowest". 
  That might help you to understand, that simple vector calculation might work and represent an idea or grammatic rule.
  
* for BPE encoded vorabulary this might apply as well, but it depends on the corpus and the number of elements in the bpe vocabulary. 
  But the calculations might also be more complex, because words are split into subwords.
  
* The transformer architecture has been proven to be working even with this fragmented words. Thus it seems to work as well. 



## Useful Resources

__Coding / Reading__
* https://blog.floydhub.com/the-transformer-in-pytorch/
  * Nice tutorial for pytorch - but also a good introduction
* https://blog.floydhub.com/gpt2/
  * Nice tutorial for GPT-2 
* https://github.com/kpot/keras-transformer
  * Building blocks of the transformer architecture implemented for keras
* https://github.com/CyberZHG/keras-gpt-2
  * Is using the mentioned keras-transformer libary
* https://github.com/ShenakhtPajouh/GPT-language-model-tf.keras/blob/master/model.py
  * different Implementation of the GPT for keras
* https://github.com/akanyaani/gpt-2-tensorflow2.0
  * implementation for GPT-2 in tensorflow 2.0
* https://towardsdatascience.com/openai-gpt-language-modeling-on-gutenberg-with-tensorflow-keras-876f9f324b6c 
* https://openai.com/blog/language-unsupervised/
* https://openai.com/blog/better-language-models/


__Model / Code__
* https://github.com/openai/gpt-2
* https://github.com/openai/gpt-2-output-dataset
* https://github.com/openai/gpt-2-output-dataset/tree/master/detector
  * Contains download code for the xl-Model
* https://blog.usejournal.com/opengpt-2-we-replicated-gpt-2-because-you-can-too-45e34e6d36dc?gi=b233c4792b2a
  * OpenGPT-2 - A replication of the GPT-2 Work on a different Dataset using a different Codebase

  
__Academic Reading__
* https://arxiv.org/abs/1706.03762  [pdf](https://arxiv.org/pdf/1706.03762)
  * (Attention is all you need) 
* https://arxiv.org/abs/1807.03819  [pdf](https://arxiv.org/pdf/1807.03819)
  * Universal Transformers
* https://arxiv.org/abs/1801.10198
* https://arxiv.org/abs/1508.07909  
  * BPE / rare word representation
* https://arxiv.org/abs/1904.07418 [pdf](https://arxiv.org/pdf/1904.07418)
  * Positional Encoding
* https://arxiv.org/abs/1511.01432
  
* Training
  * GPT
    * https://s3-us-west-2.amazonaws.com/openai-assets/research-covers/language-unsupervised/language_understanding_paper.pdf
  * GPT-2
    https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf
  * BERT
    * https://arxiv.org/abs/1810.04805
    
