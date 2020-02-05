# deepchar/entities

[github.com/deepchar/entities](https://github.com/deepchar/entities/) *Transliteration for translation of named entities*

The [transliteration](https://deepchar.github.io/) for translation of [named entities](https://en.wikipedia.org/wiki/Named_entity) is a different task than the transliteration from informal variants back into their canonical forms.  Instead of many inputs mapping to one output, one input will map to many outputs.

TODO: examples

### Our approach

TODO

#### Datasets

TODO

#### Benchmarks

TODO

#### Results

TODO

#### Future work

As a future work can be considered
 - Creating models for different combination of source and target languages, i.e. EN->RU, RU->EN, AM->RU etc.
 - Creating models for CJK (Chinese Japanese Korean) languages.
 - Research model errors dependence and transliteration quality from a token frequency.
 - Research model dependence on the lenght of named entities.
 - Evaluate models such as 
    - character-based NMT [(Ling et al., 2015)](https://arxiv.org/pdf/1808.02563.pdf)
    - convolutional Seq2Seq [(Gehring et al., 2017)](https://arxiv.org/pdf/1705.03122.pdf)<br   \>
 for named entity transliteration task.
 


### References

> *Design Challenges in Named Entity Transliteration* 2018  [arXiv](https://arxiv.org/abs/1808.02563)  
> Yuval Merhav, Stephen Ash   
> Amazon Alexa AI, Amazon AWS AI
