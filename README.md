# deepchar/entities

[github.com/deepchar/entities](https://github.com/deepchar/entities/) *Transliteration for translation of named entities*

The **[transliteration](https://deepchar.github.io/)** for translation of **[named entities](https://en.wikipedia.org/wiki/Named_entity)** is a different task than the transliteration from informal variants back into their canonical forms.  Instead of many inputs mapping to one output, **one input will map to many outputs.** 

Transliteration of named entities is useful in search engines, especially within social networks, and for legal discovery, criminal investigations and financial or governmental applications.  The goal is to find all possible versions of name, in all alphabets. 

Many names may have multiple correct transliterations within the same alphabet. So to find a friend's page on Facebook it's good to have at least few choices for a given name.

```Latn: Tagoush```➜```Armn: Թագուշ, Տագուշ, Թաքուշ```  
```Latn: Keropian```➜```Armn: Կերոպյան, Քերոբյան, Քերոպյան```  
```Latn: Roerig```➜```Armn: Ռորիգ, Ռյորիգ, Ռուրիգ```  
```Latn: Alegre```➜```Armn: Ալեգրի, Ալեգռի, էլեգրի```  
```Latn: Yershov```➜```Cyrl: Ершов, Ершев, Ерщов```  
```Latn: Savostyanov```➜```Cyrl: Савостьянов, Савостьянов, Савостианов```  
```Latn: Kruglolesskoye```➜```Cyrl: Круглолесское, Круглолеский, Круглолеской```  

Our model does a kind of query expansion. It generates all the possible "child" forms from the canocical one and outputs top three candidates.

### Types of name transliteration

The canonical cases are fairly simple.

````Armn: Հովիկ Աբրահամյան```` ➜ ````Latn: en: Hovik Abrahamyan, Hovik Abrahamian, Hovig Abrahamyan````  
````Armn: Հովիկ Աբրահամյան```` ➜ ````Cyrl: ru:Овик Абраамян, uk: Овік Абрамян````  
````Armn: Հրազդան```` ➜ ````Latn: en: Hrazdan````  
````Armn: Հրազդան```` ➜ ````Cyrl: ru: Раздан````  
````Armn: Հրազդան```` ➜ ````Cyrl: ru: Раздан````  
````Latn: Tom Collins```` ➜ ```Cyrl: ru: Том Коллинз```

Some names can have dozens of versions when transliterated into another script.

````Armn: Շողիկ Հովհաննեսի Ցոլակյան```` ➜ ````Latn: Shoghik Hovhannes Tsolakyan, Shokhik Hovhanes Tsolakian, Shoghig Hovhaness Tzolakyan````  

There are of course multiple languages per script.

````Armn: Հովիկ Աբրահամյան```` ➜ ````Latn: pl: Howik Abrahamian, de: Howik Abrahamjan````  
````Armn: Սերժ Սարգսյան```` ➜ ````Latn: en: Serzh Sargsyan, fr: Serge Sarkissian, hr: Serž Sargsjan, nl: Serzj Sarkisian````  


````Latn: John Smith```` ➜ ````Armn: hy: Ջոն Սմիթ````  
````Latn: John Smith```` ➜ ````Cyrl: ru: Джон Смит, sr: Џон Смит, uk: Джон Сміт````  
````Latn: John Smith```` ➜ ````Arab: ar:  جون سميث, fa: جان اسمیت````    
  
````Latn: SnapChat```` ➜ ````Armn: hy: Սնապչատ````  
````Latn: SnapChat```` ➜ ````Cyrl: ru: Снепчат, bg: Снапчат````  
````Latn: SnapChat```` ➜ ````Latn: tr: Snapçat, pl: Snapczat````  

#### Multiple conversions

Quite often, a name could be repeatedly transliterated.
````Armn: Հովիկ Աբրահամյան```` ➜  ````Cyrl: ru: Овик Абраамян```` ➜ ````Latn: en: Ovik Abramyan````  
````Armn: Հրազդան```` ➜ ````Cyrl: Раздан```` ➜ ````Latn: Razdan````  
````Latn: Howard Hughes```` ➜ ````Cyrl: Говард Хьюз```` ➜ ````Armn: Գովարդ Խյուզ````  

It could even come back into the original script mangled.

````Latn: Howard Hughes```` ➜ ````Cyrl: ru: Говард Хьюз```` ➜ ````Latn: Govard Khyuz````  
````Latn: Charles Aznavour```` ➜ ````Cyrl: ru: Шарль Азнавур```` ➜ ````Latn: Sharl Aznavur````  
````Armn: Հասմիկ Կուրղինյան```` ➜ ````Cyrl: ru: Асмик Кургинян```` ➜ ````Armn: Ասմիկ Կուրգինյան````   



#### Within alphabets

We can also consider some variants within the alphabet.

There are three common transcriptions for German [umlaut](https://en.wikipedia.org/wiki/Germanic_umlaut).

1. Preserve the umlaut   
````de: Müller```` ➜ ````Latn: Müller````
2. Decompose the diacritic  
````de: Müller```` ➜ ````Latn: Mueller````  
3. Simply omit the umlaut  
````de: Müller```` ➜ ````Latn: Muller````  

Decomposition is specific to German.  In many other orthographic traditions, it is simply omitted.

Some Latin orthographies nativize according to pronunciation, not unlike non-Latin alphabet orthographies.

````en: George Bush```` ➜ ````Latn: tr: Corc Buş````  
````en: George Bush```` ➜ ````Latn: de: Schorsch Busch````  
````en: George Bush```` ➜ ````Latn: sq: Xhorxh Bysh````  


## Our approach

We use an approach similar to those commonly used for translation and also our main transliteration project: **parallel corpora**.

We have trained initial models with two different architectures, **seq2seq** and **tensor2tensor**.


## Datasets

There are very limited datasets available for transliteration, let alone transliteration of named entities in all directions.

Our goal was to create an almost fully automatic data harvesting pipeline so that other researchers in the field of [NMT](https://en.wikipedia.org/wiki/Neural_machine_translation) could use it. We were motivated by the fact that at the time of this research there were very few open sources.  We extracted raw data, learned word alignment and created a dataset of multi-token name pairs.

We assumed that the pronunciation of a last name is independent of the previous tokens, and we and represent **parallel corpora** as pairs of single tokens, as in [Yuval Merhav's and Steven Ash's  approach](https://arxiv.org/pdf/1808.02563.pdf).

| Dataset  | Total size | Training size  | Source Alphabet size | Target Alphabet size | 
| :-------------: | :-------------: | :-------------: | :-------------: | :-------------: |
| Latn ➜ hy-Armn  | 39,707  | 25,412  | 152  | 107  |
| Latn ➜ ru-Cyrl  | 179,853  | 143,882  | 278  | 124  |
| Latn ➜ el-Grek  | 37,505  | 30,004  | 170  | 97  |
| Latn ➜ fa-Arab  | 78,663  | 62,930  | 170  | 117  |

The data in the Latin script included not just English but other European languages.

## Benchmarks

As benchmarks we considered the transliteration module of [Polyglot](https://pypi.org/project/polyglot/) and the bi-directional transliteration library [transliterate](https://pypi.org/project/transliterate/).


## Results

We compared [WER (Word Error Rate)](https://en.wikipedia.org/wiki/Word_error_rate) between Polyglot, and our seq2seq and tensor2tensor implementations on the given parallel corpora.

The results of the [transliterate](https://pypi.org/project/transliterate/) library are not shown because they were not competitive at all.

Interestingly, the seq2seq system consistently performed the best. The only exception is Latn ➜ el-Grek, where seq2seq and tensor2tensor had equal results.  Moreover, the tensor2tensor model failed to train on the Persian dataset.

| Dataset  | Polyglot| Seq2Seq  | Tensor2Tensor | 
| :-------------: | :-------------: | :-------------: | :-------------: |
| Latn ➜ hy-Armn  | 0.64  | **0.46**  | 0.47  |
| Latn ➜ ru-Cyrl  | 0.56  | **0.24**  | 0.37  |
| Latn ➜ el-Grek  | 0.9  | **0.52** | **0.52**  |
| Latn ➜ fa-Arab  | -  | **0.49**  | -  |

## Error analysis

Here are few examples on which shows good results.

| Task  | Source | Target  | 3-best | 
| :-------------: | :-------------: | :-------------: | :-------------: |
| Latn ➜ hy-Armn  | fazlian  | ֆազլյան  | ֆազլյան<br/>ֆասլյան<br/>ֆացլյան  |
| Latn ➜ hy-Armn  | chukhajyan  | չուխաջյան  | չուխաջյան<br/>չուխայան<br/>ճուխաջյան  |
| Latn ➜ ru-Cyrl  | afanasyeva  | афанасьева  | афанасьева<br/>афанасиева<br/>афанасева  |
| Latn ➜ ru-Cyrl  | vishnevskiĭ  | вишневский  | вишневский<br/>вышневский<br/>вишнёвский  |
| Latn ➜ ru-Cyrl  | edward  | эдвард  | эдвард<br/>эдуард<br/>эдуорд  |
| Latn ➜ el-Grek  | kioussis  | κιούσης  | κιούσης<br/>κιούσσης<br/>κιούσις  |
| Latn ➜ el-Grek  | kioussis  | κιούσης  | κιούσης<br/>κιούσσης<br/>κιούσις  |
| Latn ➜ fa-Arab  | momayez  | ممیز  | ممیز<br/>ممیظ<br/> معمیز  |
| Latn ➜ fa-Arab  | momayez  | ممیز  | ممیز<br/>ممیظ<br/> معمیز  |


## Future work

#### More directions
Creating models for different combination of source and target languages, i.e. Latn ➜ ru-Cyrl, Cyrl ➜ en-Latn, Armn ➜ ru-Cyrl, etc.

#### More script types
Creating models for scripts that use ideograms, syllabaries, such as Chinese, Japanese and Korean, or often omit vowels, such as Hebrew or Arabic.

#### Quality and confidence
Research how model errors and quality correlate with token frequency and length.

#### Context
Train models that use context, both the previous or next word or an entire sentence.

#### Architectures
Train character-based NMT [(Ling et al., 2015)](https://arxiv.org/pdf/1808.02563.pdf) or convolutional seq2seq [(Gehring et al., 2017)](https://arxiv.org/pdf/1705.03122.pdf)

#### Massive multilingual model
Train a single general model for all the languages and transliteration directions.


### References

> *Design Challenges in Named Entity Transliteration* 2018  [arXiv](https://arxiv.org/abs/1808.02563)  
> Yuval Merhav, Stephen Ash   
> Amazon Alexa AI, Amazon AWS AI
