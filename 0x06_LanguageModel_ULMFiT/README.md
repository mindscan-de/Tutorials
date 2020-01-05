# Write up for arxiv:1801.06146 -- ULMFiT-paper

This is a write up for the 'Universal Language Model Fine-tuning for Text Classification' paper of Jeremy Howard and Rebastian Ruder.

# Some context
  
This paper discusses the main ideas on NLP transfer learning which were also later used and refined in the BERT(arxiv:1810.04805), GPT and GPT-2 papers. 
Some other important ideas come from the the ELMo paper(arxiv:1802.05365), which describes some more ideas about contextual representation.
Transfer Learning became since then the state-of-the-art (SOTA) in natural language processing (NLP).

# ULMFiT

Until this paper came out there was no reliable method of transfer-learning for NLP-tasks. One field of successfully applying transfer learning before was
computer vision. Transfer learning has helped to reduce the costs of training the NLP-models by providing a good baseline trained on a large and more
general corpus and then later on, specializing/tailoring these more general models for your own purposes.   

NLP had the following issue, because of no good transfer learning until that time, all models had to be trained from scratch for each different kind 
of task and training required also always large amounts of specialized in-domain data. Such data is not always available. But there are large datasets 
of general NLP data and even huge datasets of unlabeled text available.

The proposed network architecture and retraining operation has multiple advantages
* You can train with much less in-domain training data, because the pre-trained language model has some general language understanding
  * This is especially useful, when you don't have too much labeled in-domain-data available
* You can have a general building block, which helps you to work on top of this model, providing your own new Languag tasks
  * By replacing the last layer and gradually retraining the lower layers, you can change the tasks your Model should/can achive
  * Since the model already converged to a general task, it can be easily shifted its attention to a slightly different task
* The proposed training method also provides a way to avoid catastrophic learning, where the model usually looses its ability to perform the former task, after being trained for the special task
  * This loss of ability, usually means the model is trained too much and is overfiting on the new task, and therefore looses the ability to generalize
  * The following new training techniques were proposed: discriminative fine-tuning, slanted triangular learning rates and gradual unfreezing

Both the model and the training method showed how to successfully apply pre-training and how to use pre-training models in NLP.

Since the broader availability of pre-trained NLP-Models today, NLP becomes somehow ubiquitious. 
That means that using pre-trained models became the norm in a variety of NLP-tasks such as:

* Question Answering
* Machine Translation
* Summarization
* Sentiment Classification and
* Semantic Parsing.

It becomes less of a huzzle, if your specific modifications to the task are "cheap" in terms of time and money invested, also
pre-training helps you to try more experiments. So that you can optimize the pre-trained models faster and more easily. Doing 
this from scratch will require much more engineering, experiments of different architectures, research and computational power 
as well (and someone might be luckier than you with his/her approach). Doing AI research is way more expensive, if you only want
some simple task to be done.

# Model and Training

The main idea is to have a static source task and any target task. The goal is to optimize the performancs of the target task.
Language Modeling is considered the ideal Source Task.

The objective was to implement a universal laguage model in the sense that universal means:
* It works across varaing in document size, number, and label type
* it uses a single architecture and training process
* requires no custom feature engineering or preprocessing
* it doesn't require additional in-domain documents or labels/labeled data

Stage 1 -- General-domain LM pretraining 
* Pretrain the Language Model - The objective is predicting the next word.
* Training is done on a general-domain corpus to capture general features of the languale in differert layers
* see parameters for the LanguageModel Pretraining: arxiv:1708.02182
  * Modell is an AWD-LSTM (ASGD Weight-Dropped LSTM) (ASGD - Averaged SGD) (SGD - Statistical gradient descent)
  * 3 Layer LSTM with 1150 units in the hidden Layer and an embedding dimension of 400
  * Loss is averaged over all examples and timestamps
  * embeddings wurden uniform initialisiert zwischen -0.1 und +0.1, alle anderen gewichte wurden initialisiert -1/sqrt(H) und +1/sqrt(H)
  * H is the size of the Hidden layer

Stage 2 -- Target task LM-fine-tuning
* Fine-Tune the pretrained Language Model on the new Dataset - Objective is predicting the next word. 
* Since the new dataset has different statistical characteristics, the fine-tuning step must be performed, to match the target task and characteristics.
* This will adapt the pre trained language model into your task oriented language model
* Using of the proposed techniques (same paper) "discriminative fine-tuning" and "slanted triangular learning rates"

Stage 3 -- Target Task X fine-tuning
* Train the last Layer(s) to the task you want to perform. In ULMFiT train the classifier, by replacing the last (softmax) layer with a layer/model, which is able to perform the desired target task.


