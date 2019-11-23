# BPE - Byte Pair Encoding

Back in the days when this algorithm was published and proposed as a compression method, it did not reach to much compression efficiency and 
was also quite slow because of the internal recalculation of the statistics after each compression round. It was not very effective, because 
the dictionary could only hold a few items and was limited to the amount (number) of unused bytes in a file. 

I knew this algorithm since 1997. I found its description in the C/C++ Users Journal (Volume 15, Number 9, September 1997), 
"Random Access Data Compression" by Philip Gage. Anyway there must be an earlier implementation out there, as early as February 1994 
(Philip Gage. "A New Algorithm for Data Compression", The C Users Journal, February 1994. ). I do not have this first journal. But I
still own the print version of the C/C++ Users Journal from September 1997.

Anyway this algorithm became a major building block quite recently because of its proven usefulness in NLP (Natural Language Processing) tasks 
and got even more attention because of the publishing of the GPT-2 Model. Maybe it will even evolve into a standard building block in Natural 
Language Processing.

## BPE - Algorithm

The algorithm is described by Philip Gage, as a "general-purpose lossless compression method suitable for all types of data, although this
article concentrates on text-file applications". Indeed, the author was right with the text-file applications, but differently than he 
probably ever thought of. BPE is an phrase-based-encoder using a fixed-length-coding technique, but doesn't require complex bit arithmetics 
nor variable-length bit packing.

### The compression 

The encoding requires multiple passes and after each pass the encoded data must be reanalyzed. BPE searches the most frequently occuring pair 
of adjacent bytes. It then replaces all instances of the most frequent pair with a single unused byte and stores the substitution for each
pass (dictionary). This process can be repeated until there are no more unused bytes available or until no duplicate adjacent bytes can be 
found, both mean that it is not possble to compress any further.

He described the following compression process with the following pseudocode

```
Read file into buffer
While (compression possible)
{
    Find most frequent byte pair in buffer
    
    Add pair to table and assign it an unused byte
    
    Replace all such pairs with this unused byte
}
Write pair table and buffer
```

### Some modifications to the original BPE
 
A byte can only have 256 different values. At the time of invention usually the lower half of the ASCII table was used for text representation.
Thus the bytes from 128 to 255 were considered free, when they did not appear in the text(data to compress). So the resulting dictionary had
at most 128 unused bytes, which each representing a pair of two bytes. The first unused byte was allocated for the most frequent byte pair. The
second unused byte was allocated for the second most frequent byte pair, and so on...

20 years later we don't care about unused bytes, but indexes and symbols. And we also don't care about compression at all. What we like about this 
algorithm is, its greedyness. It will identify the most frequent pairs of adjacent symbols like _('e','r')_ or _('n','t')_ and so on. Running long 
enough the most frequent adjacent symbols will join into subwords _('i', 'n', 't')_, _('i', 'o', 'n')_ or complete words like (_'p', 'u', 'b', 'l', 'i', 'c')_.
Basically each word, sentence or book can be represented either their original symbol, if it doesn't had any repetitions or an index representing two 
or more adjacent symbols.

### Speedup for large data

The most important idea is to reuse the statistics for similar texts (inputs), instead of producing the most precise one, for a particular given text 
for encoding this text. Beacuse when each text or sentence uses the same statistics, the same indexes are used for the same subwords and words.

Thus BPE became a technique to split the words into subwords or symbols(characters) according to a more general statistics and then represent 
words and sentences by a list of indexes.

Because of using the same statistics, across multiple texts (inputs), the indexes can be used for deriving useful embeddings for each index, and 
reuse the embeddings too. So the statistics essentially provides the information how to split the text(input) into subwords and words.

The calculation of the indexes, the statistics and the embeddings are computationally quite heavy (on a single machine), but this is
the environment I am currently bound to.

### The decompression

Actually we don't need it to be honest, and it depends on your implementation how easy the decoding actually is. 


## BPE - Advantages

BPE has one major advantage it can encode unknown words, which fixed dictionaries can not. Usually unknown words would be
encoded using a special token "<UNK>" or something alike.

## BPE - Disadvantages

Compared to LZ77, LZ78
* LZ77 and LZ78 assumes that each combination might be a good future candidate, and haven't seen the full stream, it builds the dictionary only 
  based on previously seen input, but LZ77 and LZ78 waste a lot of dictionary indexes at the start, whereas the BPE uses every single one with
  the most frequent first
  
* BPE goes the other way around, it requires the algorithm to see all the input to compress, and the algorithm picks the most occuring bytepair
  and replaces one pair of bytes with one unused byte. Because of the replacement of a pair with a differnt byte, the statistics for these
  element will change, and the statistics need to be recalculated. 

* but once you have collected the statistics and your byte pairs, and your source has the same stochastic properties, you can save these
  pairs and skip the calculation of the statistics, when encoding these. It might be that the compression is not at its maximum
* if you share the statistics among different encoders and the decoders, then this algorithm provides fast decoding, but slow encoding.


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
