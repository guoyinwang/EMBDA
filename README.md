# EMBeddings with Domain Awareness (EMBDA)
This repository contains source code necessary to reproduce the results presented in the paper [Learning Word Embeddings with Domain Awareness](https://arxiv.org/pdf/1805.04174.pdf).

The code is extended from origin [word2vec repository](https://github.com/tmikolov/word2vec). For more information about the origin word2vec algorith and code base requirement, please refer to [word2vec](https://code.google.com/archive/p/word2vec/).


To build the code, simply run:

`make`

The command to build word embeddings is exactly the same as in the original version, except that we removed the argument -cbow and replaced it with the argument -type:

```./embda -train input_file -word-pair-file word_pair_file -output embedding_file -type 0 -size 50 -window 5 -negative 10 -hs 0 -sample 1e-4 -threads 1 -binary 1 -iter 5```

The `-word-pair-file` option specify the file with word pairs extracted from the target domain.
Note that each line the word pair file uses the following format:
```
--------------------
w num [w1 w2 ... wn]
--------------------
```

where `w` is the word, `num` denotes how many word pairs `w` has, if `num` is not zero, then `w1 w2 ... wn` are the words paired with `w`.
Some example lines are:
```
-------
bijz 0
nsicop 0
time 10 squares callin floating winter think ...
-------
```
The lines in the word pair file should be the same with the vocabulary file for embeddings, i.e., the one use `-save-vocab` option generated.

The `-type` argument is an integer that defines which algorithm to use. These are the possible parameters:  
```
0 - the skip-gram model with domain indicator;
1 - the continuous bag-of-words with domain attention
```

