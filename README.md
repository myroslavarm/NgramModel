# Ngram Language Model

[![Build Status](https://travis-ci.org/pharo-ai/NgramModel.svg?branch=master)](https://travis-ci.org/pharo-ai/NgramModel)
[![Build status](https://ci.appveyor.com/api/projects/status/jadnl13r37s01u0v?svg=true)](https://ci.appveyor.com/project/olekscode/ngrammodel-886ci)
[![Coverage Status](https://coveralls.io/repos/github/pharo-ai/NgramModel/badge.svg?branch=master)](https://coveralls.io/github/pharo-ai/NgramModel?branch=master)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/pharo-ai/NgramModel/master/LICENSE)

## Installation

To install the packages of NgramModel, go to the Playground (Ctrl+OW) in your Pharo image and execute the following Metacello script (select it and press Do-it button or Ctrl+D):

```Smalltalk
Metacello new
  baseline: 'NgramModel';
  repository: 'github://pharo-ai/NgramModel/src';
  load.
```

## Example of text generation

#### 1. Loading Brown corpus
```Smalltalk
file := 'pharo-local/iceberg/pharo-ai/NgramModel/Corpora/brown.txt' asFileReference.
brown := file contents.
```
#### 2. Training a 2-gram language model on the corpus
```Smalltalk
model := NgramModel order: 2.
model trainOn: brown.
```
#### 3. Generating text of 100 words
At each step the model selects top 5 words that are most likely to follow the previous words and returns the random word from those five (this randomnes ensures that the generator does not get stuck in a cycle).
```Smalltalk
generator := NgramTextGenerator new model: model.
generator generateTextOfSize: 100.
```
## Result:

#### 100 words generated by a 2-gram model trained on Brown corpus
```
 educator cannot describe and edited a highway at private time ``
 Fallen Figure Technique tells him life pattern more flesh tremble 
 with neither my God `` Hit ) landowners began this narrative and 
 planted , post-war years Josephus Daniels was Virginia years 
 Congress with confluent , jurisdiction involved some used which 
 he''s something the Lyle Elliott Carter officiated and edited and
 portents like Paradise Road in boatloads . Shipments of Student 
 Movement itself officially shifted religions of fluttering soutane .
 Coolest shade which reasonably . Coolest shade less shaky . Doubts 
 thus preventing them proper bevels easily take comfort was
```
#### 100 words generated by a 3-gram model trained on Brown corpus
```
 The Fulton County purchasing departments do to escape Nicolas Manas .
 But plain old bean soup , broth , hash , and cultivated in himself , 
 back straight , black sheepskin hat from Texas A & I College and 
 operates the institution , the antipathy to outward ceremonies hailed 
 by modern plastic materials -- a judgment based on displacement of his 
 arrival spread through several stitches along edge to her paper for 
 further meditation . `` Hit the bum '' ! ! Fort up ! ! Fort up ! ! 
 Kizzie turned to similar approaches . When Mrs. Coolidge for
```
#### 100 words generated by a 3-gram model trained on Pharo source code corpus
This model was trained on the corpus composed from the source code of [85,000 Pharo methods tokenized at the subtoken level](https://github.com/pharo-ai/NgramModel/blob/master/Corpora/pharo_source.txt) (composite names like `OrderedCollection` were split into subtokens: `ordered`, `collection`)
```
 super initialize value holders . ( aggregated series := ( margins if nil
 if false ) text styler blue style table detect : [ uniform drop list input . 
 export csv label : suggested file name < a parametric function . | phase 
 <num> := bit thing basic size >= desired length ) ascii . space width + 
 bounds top - an event character : d bytes : stream if absent put : answers )
 | width of text . status value := dual value at last : category string := 
 value cos ) abs raised to n number of
```
## Warning
Training the model on the entire Pharo corpus and generating 100 words can take over 10 minutes. So start with a smaller exercise: train a 2-gram model on a Brown corpus (it is the smallest one) and generate 10 words.
