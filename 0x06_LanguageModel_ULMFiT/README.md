# Write up for arxiv:1801.06146 -- ULMFiT-paper

This is a write up for the 'Universal LanguageModel Fine-tuning for Text-Classification' paper of Jeremy Howard and Rebastian Ruder.

# Some context
  
This paper discusses the main ideas on NLP transfer learning which were also later used and refined in the BERT(arxiv:1810.04805), GPT and GPT-2 papers. 
Some other important ideas come from the the ELMo paper(arxiv:1802.05365), which describes some more ideas about contextual representation.

# ULMFiT

Until this paper came out there was no reliable method of transfer-learning for NLP-tasks. One field of successfully applying transfer learning is
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
* The proposed training method also provides a way to avoid catastrophic learning, where the model looses its ability to perform the former task, after being trained for the special task
  * This loss of ability, usually means the model is trained too much and is overfiting on the new task, and therefore looses the ability to generalize  

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
