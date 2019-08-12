# Polarity Shifter Resources
This repository contains a collection of polarity shifter resources connected to a number of publications:

- **[Schulder et al. (IJCNLP 2017)](https://github.com/uds-lsv/bootstrapped-lexicon-of-english-verbal-polarity-shifters):** Lexicon of English Verbal Shifters (bootstrapped, lemma-level) and sentiment verb phrase dataset.
- **[Schulder et al. (LREC 2018)](https://github.com/uds-lsv/lexicon-of-english-verbal-polarity-shifters):** Lexicon of English Verbal Shifters (manual, sense-level).
- **[Schulder et al. (COLING 2018)](https://github.com/uds-lsv/bootstrapped-lexicon-of-german-verbal-polarity-shifters):** Lexicon of German Verbal Shifters (bootstrapped, lemma-level).
- **[Schulder et al. (under review)](https://github.com/uds-lsv/bootstrapped-lexicon-of-english-polarity-shifters):** General Lexicon of English Shifters (bootstrapped, lemma-level).


## Data
The repository contains the following resources:
1. A general lexicon of English polarity shifters, covering verbs, adjectives and nouns. Provides lemma labels for shifters and for which polarities they can affect.
2. A lexicon of English verbal shifters. Provides word sense labels for shifters and their shifting scopes.
3. A lexicon of German verbal shifters. Provides lemma labels for shifters.
4. A set of verb phrases annotated for shifting polarities.


### 1. English Shifter Lexicon (Lemma)
A lexicon of 9145 English words, annotated for whether they are polarity shifters and which polarities they affect.
The lexicon is based on the vocabulary of WordNet v3.1 (Miller et al., 1990).
It contains 2631 shifters and 6514 non-shifters.

- File: `shifters.english.all.lemma.txt`
- The lexicon is a comma-separated value (CSV) table.
- Each line follows the format `POS,LEMMA,SHIFTER_LABEL,DIRECTION_LABEL,SOURCE`.
  - `POS`: The part of speech of the word (`verb`, `noun`, `adj`)
  - `LEMMA`: The lemma representation of the word in question. Multiword expressions are separated by an underscore (`WORD_WORD`).
  - `SHIFTER_LABEL`: Whether the word is a polarity shifter (`SHIFTER`) or a non-shifter (`NONSHIFTER`).
  - `DIRECTION_LABEL`: Whether the shifter affects only positive polarities (`AFFECTS_POSITIVE`), only negative polarities. (`AFFECTS_NEGATIVE`) or can shift in both directions (`AFFECTS_BOTH`). Non-shifters are all labeled (`NONE`).
  - `SOURCE`: Whether the word was part of the gold standard. (`GOLD_STANDARD`) or was bootstrapped (`BOOTSTRAPPED`). Note that while bootstrapped shifter labels are verified by a human annotator, their direction label is automatically classified without verification.

### 2. English Verbal Shifter Lexicon (Word Sense)
A lexicon of word senses of English verbs, annotated for whether they are polarity shifters and their shifting scope.
The lexicon covers all verbs of WordNet v3.1 (Miller et al., 1990) that are single word or particle verbs.
Polarity shifter and scope labels are given for each lemma-synset pair (i.e. each word sense of a lemma).

The data is presented in the following forms:
1. A complete lexicon of all verbal shifters and their shifting scopes.
2. Two auxiliary lists containing simplified information:
    1. A list of all lemmas with shifter labels
    2. A list of all word senses with shifter labels

All files are in CSV (comma-separated value) format.

#### 2.1. Complete Lexicon
The main lexicon lists all verbal shifters and their shifting scopes.
Verbal shifters are modeled as lemma-sense pairs with one or more shifting scopes.

The lexicon lists all lemma-sense pairs that are verbal shifters.
Any lemma-sense pair not listed is not a verbal shifter.
When a lemma-sense pair has more than one possible scope, a separate entry is made for each scope.

- File name: `shifters.english.verb.sense.csv`
- Each line contains a single lemma-sense-scope triple, using the format `LEMMA,SYNSET,SCOPE`.
  - `LEMMA`: The lemma representation of the verb in question. Multiword expressions are separated by an underscore (`WORD_WORD`).
  - `SYNSET`: The numeric identifier of the synset, commonly referred to as _offset_ or _database location_. It consists of 8 digits, including leading zeroes (e.g. `00334568`).
  - `SCOPE`: The scope of the shifting:
    - `subj`: The verbal shifter affects its subject.
    - `dobj`: The verbal shifter affects its direct object.
    - `pobj_*`: The verbal shifter affects objects within a prepositional phrase. The preposition in question is included in the annotation. For example a _from_-preposition scope receives the label `pobj_from` and a a _for_-preposition receives `pobj_for`.
    - `comp`: The verbal shifter affects a clausal complement, such as infinitive clauses or gerunds.

#### 2.2. List of Lemmas
List of all verb lemmas and whether they are shifters in at least one of their word senses.
Does not provide shifter scope information.

Many verbal shifter lemmas only cause shifting in some of their word senses.
This list is therefore considerably more coarse-grained than the main lexicon.
It is intended as a convenience measure for quick experimentation.

- File name: `shifters.english.verb.sense.lemmas_only.csv`
- Each line follows the format `LEMMA,SHIFTER_LABEL`.
  - `LEMMA`: The lemma representation of the verb in question. Multiword expressions are separated by an underscore (`WORD_WORD`).
  - `SHIFTER_LABEL`: Whether the verb is a polarity shifter (`SHIFTER`) or a non-shifter (`NONSHIFTER`).

#### 2.3. List of Synsets
List of all synsets and whether their lemmas are shifters in this specific word sense.
Does not provide shifter scope information.

Shifting is shared among lemmas of the same word sense.
This list, therefore, provides (almost) the same granularity for the shifter label as the main lexicon.
However, in a few exceptions, synsets contained words with subtly different senses that did not all cause shifting.
These senses are considered shifters in this list, analogous to the generalization in the list of lemmas.

- File name: `shifters.english.verb.sense.synsets_only.csv`
- Each line follows the format `SYNSET,SHIFTER_LABEL`.
  - `SYNSET`: The numeric identifier of the synset, commonly referred to as _offset_ or _database location_. It consists of 8 digits, including leading zeroes (e.g. `00334568`).
  - `SHIFTER_LABEL`: Whether the verb is a polarity shifter (`SHIFTER`) or a non-shifter (`NONSHIFTER`).

### 3. German Verbal Shifter Lexicon (Lemma)
A lexicon of 2595 German verbs, annotated for whether they are polarity shifters and which polarities they affect.
The lexicon is based on the vocabulary of GermaNet (Hamp and Feldweg, 1997).
It contains 677 shifters and 1918 non-shifters.

- File: `shifters.german.verb.lemma.txt`
- The lexicon is a comma-separated value (CSV) table.
- Each line follows the format `LEMMA,SHIFTER_LABEL,SOURCE`.
  - `LEMMA`: The lemma representation of the verb in question. Multiword expressions are separated by an underscore (`WORD_WORD`).
  - `SHIFTER_LABEL`: Whether the verb is a polarity shifter (`SHIFTER`) or a non-shifter (`NONSHIFTER`).
  - `SOURCE`: Whether the word was part of the gold standard. (`GOLD_STANDARD`) or was bootstrapped (`BOOTSTRAPPED`). In either case the verbs were verified by a human annotator.

### 4. Sentiment Verb Phrases
A set of verb phrases, annotated for the polarity of the verb phrase and the polarity of a polar noun that it contains.
Can be used to evaluate whether a polarity classifier correctly recognizes polarity shifting.
The file starts with 400 phrases containing shifter verbs, followed by 2231 phrases containing non-shifter verbs.

- File:  `sentiment_phrases.txt`
- Every item consists of:
  - The sentence from which the VP and the polar noun were extracted.
  - The VP, polar noun and the verb heading the VP.
  - Constituency parse for the VP.
  - Gold labels for VP and polar noun by a human annotator.
  - Predicted labels for VP and polar noun by RNTN tagger (Socher et al., 2013) and `LEX_gold` approach.
  - Items are separated by a line of asterisks (*)

## Attribution
This data set is published under [Creative Commons Attribution 4.0](https://github.com/uds-lsv/bootstrapped-lexicon-of-english-verbal-polarity-shifters/blob/master/LICENSE).

## Acknowledgements
This work was partially supported by the German Research Foundation (DFG) under grants RU 1873/2-1 and WI4204/2-1.

## References
B. Hamp and H. Feldweg: "GermaNet - a Lexical-Semantic Net for German", in Proceedings of the ACL Workshop Automatic Information Extraction and Building of Lexical Semantic Resources for NLP Applications, 1997.

N. Jindal and B. Liu: "Opinion Spam and Analysis", in Proceedings of ACM-WSDM, 2008.

G. Miller, R. Beckwith, C. Fellbaum, D. Gross, K. Miller: "Introduction to WordNet: An On-Line Lexical Database". International Journal of Lexicography (3), 1990.

M. Schulder, M. Wiegand, J. Ruppenhofer and B. Roth (2017). "Towards Bootstrapping a Polarity Shifter Lexicon using Linguistic Features", in Proceedings of IJCNLP, 2017.

M. Schulder, M. Wiegand, J. Ruppenhofer and S. Köser (2018). "Introducing a Lexicon of Verbal Polarity Shifters for English", in Proceedings of LREC,  2018.

M. Schulder, M. Wiegand and J. Ruppenhofer (2018). "Automatically Creating a Lexicon of Verbal Polarity Shifters: Mono- and Cross-lingual Methods for German", in Proceedings of COLING, 2018.

M. Schulder, M. Wiegand and J. Ruppenhofer (to be submitted). "Bootstrapped Creation of a Lexicon of Sentiment Polarity Shifters".

R. Socher, A. Perelygin, J. Wu, J. Chuang, C. Manning, A. Ng, C. Potts: "Recursive Deep Models for Semantic Compositionality Over a Sentiment Treebank", in Proceedings of EMNLP, 2013.
