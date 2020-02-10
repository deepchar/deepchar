# deepchar/entities

[github.com/deepchar/entities](https://github.com/deepchar/entities/) *Transliteration for translation of named entities*

The [transliteration](https://deepchar.github.io/) for translation of [named entities](https://en.wikipedia.org/wiki/Named_entity) is a different task than the transliteration from informal variants back into their canonical forms.  Instead of many inputs mapping to one output, one input will map to many outputs.

### Types of name transliteration tasks:

#### Simple
````Armn: Հովիկ Աբրահամյան````=>````Latn: en: Hovik Abrahamyan, Hovik Abrahamian, Hovig Abrahamyan````<br/>
````Armn: Հովիկ Աբրահամյան````=>````Cyrl: ru:Овик Абраамян, uk: Овік Абрамян````<br/>
````Armn: Հրազդան````=>````Latn: en: Hrazdan````<br/>
````Armn: Հրազդան````=>````Cyrl: ru: Раздан````<br/>

Some names can have dozens of versions into one script:

````Armn: Շողիկ Հովհաննեսի Ցոլակյան````=>````Latn: Shoghik Hovhannes Tsolakyan, Shokhik Hovhanes Tsolakian, Shoghig Hovhaness Tzolakyan````<br/>

There are of course multiple languages per script.

````Armn: Հովիկ Աբրահամյան````=>````Latn: pl: Howik Abrahamian, de: Howik Abrahamjan````<br/>
````Armn: Սերժ Սարգսյան````=>````Latn: en: Serzh Sargsyan, fr: Serge Sarkissian, hr: Serž Sargsjan, nl: Serzj Sarkisian````<br/>


````Latn: John Smith````=>````Armn: hy: Ջոն Սմիթ````<br/>
````Latn: John Smith````=>````Cyrl: ru: Джон Смит, sr: Џон Смит, uk: Джон Сміт````<br/>
````Latn: John Smith````=>````Arab: ar:  جون سميث, fa: جان اسمیت````<br/>  
  
````Latn: SnapChat````=>````Armn: hy: Սնապչատ````<br/>
````Latn: SnapChat````=>````Cyrl: ru: Снепчат, bg: Снапчат````<br/>
````Latn: SnapChat````=>````Latn: tr: Snapçat, pl: Snapczat````<br/>

#### Multiple conversions

````Armn: Հովիկ Աբրահամյան````=> ````Cyrl: ru: Овик Абраамян````=>````Latn: en: Ovik Abramyan````<br/>
````Armn: Հրազդան````=>````Cyrl: Раздан````=>````Latn: Razdan````<br/>
````Latn: Howard Hughes````=>````Cyrl: Говард Хьюз````=>````Armn: Գովարդ Խյուզ````<br/>


It could come back into the original script mangled:

````Latn: Howard Hughes````=>````Cylr: ru: Говард Хьюз````=>````Latn: Govard Khyuz````<br/>
````Armn: Հասմիկ Կուրղինյան````=>````Cyrl: ru: Асмик Кургинян````=>````Armn: Ասմիկ Կուրգինյան````<br/> 

#### Within alphabets

Let's consider some linguistic variations within the alphabet in case of the German name Müller. There are three common transcriptions for German [umlaut](https://en.wikipedia.org/wiki/Germanic_umlaut).
1. the umlaut stays<br/> 
````de: Müller````=>````Latn: Müller````
2. diacritic replaced by an *e* after the vowel so that *ü* becomes *ue*<br/>
````de: Müller````=>````Latn: Mueller````<br/>
3. the umlaut diacritic is simply omitted, and *ü* becomes *u*<br/> 
````de: Müller````=>````Latn: Muller````<br/>

Name Goerge Bush provides a list of variations within the same latin script:

````en: George Bush````=>````Latn: tr: Corc Buş````<br/>
````en: George Bush````=>````Latn: de: Schorsch Busch````<br/>
````en: George Bush````=>````Latn: de: Schorsch Bussche````<br/>
````en: George Bush````=>````Latn: en: George Boush````<br/>
````en: George Bush````=>````Latn: alb: Xhorxh Bysh````<br/>


## Our approach

We use an approach similar to those commonly used for translation and also our main transliteration project: **parallel corpora**.

We have trained initial models with two different architectures, **seq2seq** and **tensor2tensor**


## Datasets

Dataset creation is one of the most expensive tasks in [NLP](https://en.wikipedia.org/wiki/Natural_language_processing). Our goal was to create an almost 100% data collection pipeline so that other researchers in the field of [NMT](https://en.wikipedia.org/wiki/Neural_machine_translation) could use it. We were motivated by the fact that at the time of this research there were very few open-sources.
We extracted raw data, learned word alignment and created a dataset of multi-token name pairs. We assumed that the pronunciation of a last name is independent of the previous tokens we stick with [Yuval Merhav's and Steven Ash's  approach ](https://arxiv.org/pdf/1808.02563.pdf) and represent **parallel corpora** as a single tokens pair. 
Table below shows dataset statistics. Here EN means latin scripts not only English.

| Dataset  | Total size | Training size  | Source Alphabet size | Target Alphabet size | 
| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: |
| EN-HY  | 39,707  | 25,412  | 152  | 107  |
| EN-RU  | 179,853  | 143,882  | 278  | 124  |
| EN-EL  | 37,505  | 30,004  | 170  | 97  |
| EN-FA  | 78,663  | 62,930  | 170  | 117  |


## Benchmarks
As a benchmark we considered multilingal NLP pipeline [Polyglot](https://pypi.org/project/polyglot/) and bi-directional transliterator [transliterate](https://pypi.org/project/transliterate/).


## Results

Table below shows [WER (Word Error Rate)](https://en.wikipedia.org/wiki/Word_error_rate) comparison for Polyglot, Seq2Seq and Tensor2Tensor on the given parallel corpora. Results of the [transliterate](https://pypi.org/project/transliterate/) library are not shown because they were very far below displayed ones. Interestingly, the seq2seq system consistently performed the best. The only exception is EN=>EL Seq2Seq and Tensor2Tensor show equal results. Moreover,  Tensor2Tensor model failed to train on persian dataset.

| Dataset  | Polyglot| Seq2Seq  | Tensor2Tensor | 
| :-------------: | :-------------: | :-------------: | :-------------: |
| EN=>HY  | 0.64  | **0.46**  | 0.47  |
| EN=>RU  | 0.56  | **0.24**  | 0.37  |
| EN=>EL  | 0.9  | **0.52** | **0.52**  |
| EN=>FA  | -  | **0.49**  | -  |

## Future work

As a future work can be considered
 - Creating models for different combination of source and target languages, i.e. EN->RU, RU->EN, AM->RU etc.
 - Creating models for CJK (Chinese Japanese Korean) languages.
 - Research model errors dependence and transliteration quality from a token frequency.
 - Research model dependence on the lenght of named entities.
 - Evaluate models such as 
    - character-based NMT [(Ling et al., 2015)](https://arxiv.org/pdf/1808.02563.pdf)
    - convolutional Seq2Seq [(Gehring et al., 2017)](https://arxiv.org/pdf/1705.03122.pdf)<br/>
    for named entity transliteration task.
 - Create genereal model for all the languages


### References

> *Design Challenges in Named Entity Transliteration* 2018  [arXiv](https://arxiv.org/abs/1808.02563)  
> Yuval Merhav, Stephen Ash   
> Amazon Alexa AI, Amazon AWS AI
