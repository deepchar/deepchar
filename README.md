# deepchar/entities

[github.com/deepchar/entities](https://github.com/deepchar/entities/) *Transliteration for translation of named entities*

The [transliteration](https://deepchar.github.io/) for translation of [named entities](https://en.wikipedia.org/wiki/Named_entity) is a different task than the transliteration from informal variants back into their canonical forms.  Instead of many inputs mapping to one output, one input will map to many outputs.

### Types of name transliteration tasks:

#### Simple
````hy: Հովիկ Աբրահամյան````=>````en: Hovik Abrahamyan, Hovik Abrahamian, Hovig Abrahamyan````<br/>
````hy: Հովիկ Աբրահամյան````=>````cyrl: ru:Овик Абраамян, uk: Овік Абрамян````<br/>
````hy: Հրազդան````=>````en: Hrazdan````<br/>
````hy: Հրազդան````=>````ru: Раздан````<br/>

Some names can have dozens of versions into one script:

````hy: Շողիկ Հովհաննեսի Ցոլակյան````=>````en: Shoghik Hovhannes Tsolakyan, Shokhik Hovhanes Tsolakian, Shoghig Hovhaness Tzolakyan````<br/>

There are of course multiple languages per script.

````hy: Հովիկ Աբրահամյան````=>````la: pl: Howik Abrahamian, de: Howik Abrahamjan````<br/>
````hy: Սերժ Սարգսյան````=>````la: en: Serzh Sargsyan, fr: Serge Sarkissian, hr:Serž Sargsjan, nl: Serzj Sarkisian````<br/>


````la: John Smith````=>````hy: Ջոն Սմիթ````<br/>
````la: John Smith````=>````cyrl: ru: Джон Смит, sr: Џон Смит, uk: Джон Сміт````<br/>
````la: John Smith````=>````ar: ar:  جون سميث, fa: جان اسمیت````<br/>  
  
````la: SnapChat````=>````hy: Սնապչատ````<br/>
````la: SnapChat````=>````cyrl: ru: Снепчат, bg: Снапчат````<br/>
````la: SnapChat````=>````la: tr: Snapçat, pl: Snapczat````<br/>

#### Multiple conversions

````hy: Հովիկ Աբրահամյան````=> ````cyrl: ru: Овик Абраамян````=>````la: en: Ovik Abramyan````<br/>
````hy: Հրազդան````=>````cyrl: ru: Раздан````=>````la: en: Razdan````<br/>
````la: en: Howard Hughes````=>````cyrl: ru: Говард Хьюз````=>````hy: Գովարդ Խյուզ````<br/>


It could come back into the original script mangled:

````la: Howard Hughes````=>````cyrl: ru: Говард Хьюз````=>````la: en: Govard Khyuz````
````hy: Հասմիկ Կուրղինյան````=>````cyrl: ru: Асмик Кургинян````=>````hy: Ասմիկ Կուրգինյան````<br/> 

#### Within alphabets

````en: Müller````=>````de: Müller, Mueller, Muller````<br/>
````la: George Bush````=>````tr: George Bush, Corc Buş````<br/>

## Our approach

We use an approach similar to those commonly used for translation and also our main transliteration project: **parallel corpora**.

We have trained initial models with two different architectures, **seq2seq** and **tensor2tensor**

The **parallel corpora** have XK lines per script pair?.


## Datasets

TODO

## Benchmarks

TODO

## Results

TODO

## Future work

As a future work can be considered
 - Creating models for different combination of source and target languages, i.e. EN->RU, RU->EN, AM->RU etc.
 - Creating models for CJK (Chinese Japanese Korean) languages.
 - Research model errors dependence and transliteration quality from a token frequency.
 - Research model dependence on the lenght of named entities.
 - Evaluate models such as 
    - character-based NMT [(Ling et al., 2015)](https://arxiv.org/pdf/1808.02563.pdf)
    - convolutional Seq2Seq [(Gehring et al., 2017)](https://arxiv.org/pdf/1705.03122.pdf)<br   />
 for named entity transliteration task.
 


### References

> *Design Challenges in Named Entity Transliteration* 2018  [arXiv](https://arxiv.org/abs/1808.02563)  
> Yuval Merhav, Stephen Ash   
> Amazon Alexa AI, Amazon AWS AI
