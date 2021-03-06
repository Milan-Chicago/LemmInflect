# Accuracy of the Lemmatizer

The accuracy of LemmInflect and several other popular NLP utilities was tested using the [Automatically Generated Inflection Database (AGID)](http://wordlist.aspell.net/other) as a baseline.  The AGID has an extensive list of lemmas and their corresponding inflections.  Each inflection was lemmatized by the test software and then compared to the original value in the corpus. The test included 119,194 different inflected words.

## Results
```
| Package          | Verb  |  Noun | ADJ/ADV | Overall |  Speed  |
|----------------------------------------------------------------|
| LemmInflect      | 96.1% | 95.4% |  93.9%  |  95.6%  | 42.0 uS |
| CLiPS/pattern.en | 93.6% | 91.1% |   0.0%  |  n/a    |  3.0 uS |
| Stanford CoreNLP | 87.6% | 93.1% |   0.0%  |  n/a    |  n/a    |
| spaCy            | 79.4% | 88.9% |  60.5%  |  84.7%  |  5.0 uS |
| NLTK             | 53.3% | 52.2% |  53.3%  |  52.6%  | 13.0 uS |
|----------------------------------------------------------------|
```
* Speed is in micro-seconds per lemma and was conducted on a i9-7940x CPU.
* The Stanford and CLiPS lemmatizers don't accept part-of-speech information and in the case of the pattern.en, the methods was setup specifically for verbs, not as a lemmatizer for all word types.
* The Stanford CoreNLP lemmatizer is a Java package and testing was done via the built-in HTML server, thus the speed measurement is invalid.

## Notes on test conditions:
The test corpus has almost 120K words, which is more than the typical vocabulary.  It's likely the software packages tested will not have many of these words in their online corpus.  Because of this, the words will be treated as "out-of-vocabulary" which generally produces less reliable lemmatization.  Re-running tests with a smaller vocabulary will yield higher scores across the tested packages.

The corpus does not include the lemma itself as a test case.  In some software tasks you may lemmatize a lemma but those conditions are not simulated here.  Including lemmas in the test corpus yields higher scores across-the-board.
