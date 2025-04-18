### Notes

#### Chapter 2: Understanding Foundational Models

- Picking out the most common output among a set of outputs can be especially
  useful for tasks that expect exact answers.
- To get a model to give structured output we can give it instructions i.e
  prompting. We can do that and some manual post-processsing where we have a
  script etc fix small mistakes. We can also do something called constrain
  sampling. This is expensive and non-trivial. Finetuning is the best bang for
  your buck approach to get the expected output. But as modles get better at
  following instructions prompting will probably be enough in the future

#### Chapter 3: Evalutation Methodology
There are a couple of different metrics used to develop language models 
- Entropy, measures how much informatio on averag a token carries. The higher
  the entropy, the more information each token carries and the more bits are
  needed to represent a token. For example say you have a languge to describe
  position in a square, it can be A or B. One bit is enough in this case to
  represent the positon in this language, thus this language has entropy of 1.
- Cross Entropy, is the measure of how difficult it is for the language model to
  predict what comes next in the dataset it was trained on. The two main
  components of cross entropy is:
  a) The training data's predictability, measures by the training data's entropy
  b) How the distribution captured by the language model diverges from the true
     distribution of the training data.
  A language models is trained to minimize it's cross entropy with respect to
  the training data. If the language model learns perfectly from it's training
  data, the models cross entropy will be exactly the same as the entropy of the
  training data. The kullback-leibler (KL) divergence will then be 0.
- Bits-per-character(BPC) and Bits-per-byte(BPB): one unit of entropy and cross
  entropy is bits. If the cross entropy of a language model is 6 bits, this
  language model needs 6 bits to represent each token.
  
  Since language models have different tokenization techniques we usually talk
  about BPC and BPB instead. If number of bits per token is 6 and on average,
  each token is 2 charachters, BCP = 6/2 = 3.
  But characthers can have different encoding schemas which makes BPC a hard
  measure to standardize. Instead with BPB we have the number of bits a language
  models needs to represent one byte of the original training data. If the BPC
  is 3 and each character is 7 bits or 7/8 of a byte, then BPB is 3/(7/8) 3.43.
  
  Cross entropy tells us how efficient a language model will be at compressing.
  For example if BPB is 3.43 it means that it can represent each byte in the
  original text with 3.43 bits. Thus it can compress the original text to less
  than half its size.
- Perplexity, if cross entropy measures how difficult it is to predict the next
  token, perplexity measure the amount of uncertainty it when predicting the
  next token. Higher uncertainty means tere are more possible options for the
  next token. In the square example if we could have 4 positons instead and thus
  needing 2 bits i.e and Entropy of 2. Then for a model to predict a position in
  that language it has 4 possibilites, thus the perplexity of that model is 4.

#### Evaluation Strategies
  

---
status: :📖:
tags: [[Book notes]] - [[030 Software Development.md]] - [[001 Book Index.md]]
date: 2025-04-18
