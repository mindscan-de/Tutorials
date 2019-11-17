# BPE - Byte Pair Encoding

Back in the days where this algorithm was published, and proposed as a compression method it did not reach to much compression and 
was quite slow because of the recalculation of the statistics. Since the dictionary could only hold a few items and was limited to 
the amount (number) of unused bytes in a file.

I used to know this algorithm since 1997, when I found its description in the C/C++ Users Journal (Volume 15, Number 9, September 1997), 
"Random Access Data Compression" by Philip Gage. Anyway there must be an earlier implementation out there, as early as February 1994 
(Philip Gage. "A New Algorithm for Data Compression," The C Users Journal, February 1994. ). But I do not have this journal. But I
still have the print version of the C/C++ Users Journal from September 1997.

Anyway this algorithm became a major building block recently because of its usefulness in NLP (Natural Language Processing) tasks 
and got even more attention because of the publishing of the GPT-2 Model.

## Useful Resources

__Reading__
* https://www.drdobbs.com/2441/DrDobbs/random-access-data-compression/184403389?pgno=2
  * 
* https://medium.com/@makcedward/how-subword-helps-on-your-nlp-model-83dd1b836f46
  * Introduction and description of BPE in the context of the GPT-2 Model
* https://towardsdatascience.com/3-silver-bullets-of-word-embedding-in-nlp-10fa8f50cc5a
  * Word embeddings
* https://towardsdatascience.com/besides-word-embedding-why-you-need-to-know-character-embedding-6096a34a3b10
  * Character embedding
  
  
__Academic Reading__
* https://arxiv.org/pdf/1808.06226.pdf
* http://aclweb.org/anthology/P16-1162
