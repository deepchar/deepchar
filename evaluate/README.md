# Evaluate


### Basic
The basic benchmark 

### Noisy

In the real world, there are 4 basic types of input.

For example, if we 

1. Translit

`naprimer` => `например`

2. Target

`например` => `например`

3. 3rd languages

`for example` => `for example`

4. 3rd scripts

`例如` => `例如`

1 is the main focus of transliteration.  2, 3 and 4 the model should pass through untouched, but the model must learn to distinguish 3 from 1.

### Multiple pairs: multiple sources

We can train a model that converts multiple source scripts into the target script and language.

`նապրիմեր` => `например`

See also: [Transfer learning](https://deepchar.github.io/#transfer-learning))

### Multiple pairs: multiple targets

We can train a model that converts multiple languages in the source script into multiple target scripts and languages.

`naprimer` => `например`  
`orinak` => `օրինակ`

In this flavour of the task, the model is implicitly learning [language identification](https://en.wikipedia.org/wiki/Language_identification).

## Metrics

How do we evaluate different outputs?

For example if the golden output is `например Москва и Питер`, and the outputs of the models we are evaluating are:

`на пример Москва и Питер`

`например Масква и Петер`

`например Москва и Peter`

Which is more correct?  What should the score be for each on a scale of 0.0 to 1.0?

### Exact match

TODO

### Character-level BLEU

TODO

### More

TODO

## Interpretability and Visualisation

Ideally on both test and validation sets we would see not just the aggregate score, but breakdowns by noise types, length, word frequency and so on, as well as a list of the sentences and words that had the worst scores.

