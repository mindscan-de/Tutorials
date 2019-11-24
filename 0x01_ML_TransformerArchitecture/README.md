# The Transformer Architecture

![The Transformer - model architecture][TransformerModelArchitecture]

## Basics

The basic building blocks (layers) of the transformer architecture are:

* Embedding the input and output vocabulary
* Positional encodings
* Masking
* Attention
* Feed-Forward-Networks
* Normalization

### Embedding the input and output vocabulary

Embedding is one step when working on natural language processing. 
A given text is split into tokens and each token will then be feed into a model.
The model will perform its calculations on float numbers instead of discrete integers.
Each token is replaced by a vector of float numbers having usually 300 dimensions or more.
Newer and more precise models have more than 1000 dimensions, for each individual token.
This replacement (of the index) of the token is called embedding.
The embeddings are calculated using large corpora of texts and then trained via GlovalVectors (GloVe), FastText or Word2Vec.   

If you are going to implement a machine translation system, you may have two languages involved, the source language (e.g. english) and the destination language (e.g. german).
Both of them have a different vocabulary and different statistics also have different embeddings.  

But there are also valid configurations, where the source and the destination language are the same. 
Like when you want to predict the next words of an english input.
Then you use the same vocabulary as your input and output vocabulary and the same embeddings for the vorabulary. 

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

## Positional Encodings

For a model being able to determine the meaning of a word in a sentence, we must provide two things to the model:  

* What is the meaning of the word?
* What is the position of the word in the sentence?

The question for the meaning is already answered by using the embeddings for each word or token. 
The second question for the position in the sentence is a bit harder, but not too hard.
We have to add this kind of information to each word/token in the sentence.
We do that by simply watermarking the words with a nonrepeating pattern, which the model can also learn.

The sentence may have a different meaning, depending of the position of words in the sentence. 
The sentence "ich liebe dich!" (i love you!) has a different meaning than the sentence "liebe ich dich?" ((do) i love you?).
As seen the position of a word is of imortance, even the position of a comma, might change the meaning of a sentence completely, so the model must know at which position a comma was set.   

If you like you can also refer to the papers _"Attention is all you need"_, A. Vaswani et al., section 3.5, (2017), as well as this one where encoding also mentioned in _"Positional Encoding to Control Output Sequence Length"_, 2019. 
You may also have a look into the ipython notebook in the FluentGenesis-Classifer Project.

For reasons of simplicity it's enough to stick to the most simple implementation right now. 

For all even dimensions calculate:

	PE(pos, 2i) = sin(pos/( 10000^(2i/d_model)))
	
For all odd dimensions calculate:

    PE(sin, 2i+1) = cos(pos/( 10000^(2i/d_model)))

Whereas pos is the position of a word in a sentence, and i is the dimension of the vector element.


## Implementing the Transformer Architecture

*Maybe better to not implement it on my own...* but instead use already implemeted building blocks and examples. Maybe have to rework the training. 
I still haven't mastered implementing a transformer like architecture on my own, using only the paper.
 


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
  * _"Attention is all you need"_,  A. Vaswani et al., 2017.
* https://arxiv.org/abs/1807.03819  [pdf](https://arxiv.org/pdf/1807.03819)
  * Universal Transformers
* https://arxiv.org/abs/1801.10198
* https://arxiv.org/abs/1508.07909  
  * BPE / rare word representation
* https://arxiv.org/abs/1904.07418 [pdf](https://arxiv.org/pdf/1904.07418)
  * _"Positional Encoding to Control Output Sequence Length"_, Sho Takase and Naoaki Okazaki, 2019.
* https://arxiv.org/abs/1511.01432
  
* Training
  * GPT
    * https://s3-us-west-2.amazonaws.com/openai-assets/research-covers/language-unsupervised/language_understanding_paper.pdf
  * GPT-2
    https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf
  * BERT
    * https://arxiv.org/abs/1810.04805
    
[TransformerModelArchitecture]: arxiv1706.03762.the_transformer_model_architecture.figure1.png "The Transformer - model architecture / Source: A. Vaswani et al. 'Attention is all you need'"
[PositionalEncoding]: positional_encoding.png "Positional Encoding for 512 positions and a dimensional embedding vectors. / Source: self." 