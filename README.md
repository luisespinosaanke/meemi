## Meemi

The following repository includes the code and pre-trained cross-lingual word embeddings from the paper *[Improving cross-lingual word embeddings by meeting in the middle](https://arxiv.org/abs/1808.08780)*  (EMNLP 2018).


### Pre-trained embeddings

We release the 300-dimension word embeddings used in our experiments as binary *bin* files:

- **Monolingual FastText embeddings**: Available [here](https://drive.google.com/drive/folders/1sQNZN4_2GRkK0Pb1pRJaOpM6Nh8yHJpX?usp=sharing)
- **Baseline cross-lingual embeddings**: Available [here](https://drive.google.com/drive/folders/1Qq5_fC9kqWUA_YwP3SLPpjCB_KMNvxlB?usp=sharing)
- **Cross-lingual embeddings post-processed with Meemi**: Available [here](https://drive.google.com/drive/folders/1q0SijS7dcPqN0_N3Ct5_GTKDu3N-_5xB?usp=sharing)

*Note 1:* All vocabulary words are lowercased.

*Note 2:* If you would like to convert the binary files to *txt*, you can use [convertvec](https://github.com/marekrei/convertvec).


**Requirements:**

- Python 3
- NumPy
- Gensim
- If you use [VecMap](https://github.com/artetxem/vecmap) or [MUSE](https://github.com/facebookresearch/MUSE), please also check their corresponding GitHub pages. Note that we use a previous version of these tools, of which there is a copy in this repository (WIP).

### Usage

```bash
get_crossembs.sh SOURCE_EMBEDDINGS TARGET_EMBEDDINGS DICTIONARY_FILE [-vecmap | -muse TRAIN_DICT VALID_DICT]
```

#### Apply meemi to your cross-lingual embeddings

```bash
get_crossembs.sh SOURCE_EMBEDDINGS TARGET_EMBEDDINGS DICTIONARY_FILE
```

#### Use VecMap to align monolingual embeddings and then meemi

```bash
get_crossembs.sh SOURCE_EMBEDDINGS TARGET_EMBEDDINGS DICTIONARY_FILE -vecmap
```

#### Use MUSE to align monolingual embeddings and then meemi

```bash
get_crossembs.sh SOURCE_EMBEDDINGS TARGET_EMBEDDINGS DICTIONARY_FILE -muse TRAIN_SIZE VALID_SIZE
```

### Experiments


#### Bilingual Dictionary Induction

In order to test your embeddings on **bilingual dictionary induction** type the following:

```bash
python test.py SOURCE_EMBEDDINGS TARGET_EMBEDDINGS < DICTIONARY_FILE
```

#### Word similarity

In order to test your embeddings on **monolingual word similarity** type the following:

```bash
python test_similarity_monolingual.py EMBEDDINGS DATASET
```
You can also test various datasets at the same time:

```bash
python test_similarity_monolingual.py EMBEDDINGS DATASET1 [DATASET2] ... [DATASETN]
```
Likewise, to test your cross-lingual embeddings on **cross-lingual word similarity** type the following:

```bash
python test_similarity_crosslingual.py SOURCE_EMBEDDINGS TARGET_EMBEDDINGS DATASET
```
As with monolingual similarity, you can also test various datasets at the same time. Below is an example of how to test your English-Spanish cross-lingual embeddings on all the monolingual and cross-lingual word similarity datasets:

```bash
python test_similarity_monolingual.py EN-ES.english.vecmap.meemi.bin data/SimLex/simlex-999_english.txt data/SemEval2018-subtask1-monolingual/english.txt data/rg65-monolingual/rg65_english.txt data/WS353-monolingual/WS353-english-sim.txt
python test_similarity_monolingual.py EN-ES.english.vecmap.meemi.bin data/SemEval2018-subtask1-monolingual/spanish.txt data/rg65-monolingual/rg65_spanish.txt 
python test_similarity_crosslingual.py EN-ES.english.vecmap.meemi.bin EN-ES.spanish.vecmap.meemi.bin data/SemEval2018-subtask2-crosslingual/en-es.txt data/rg65-crosslingual/rg65_EN-ES.txt
```
*Note:* This code assumes that lowercased word embeddings are provided as input. If you would like to mantain the casing, simply remove the *.lower()* commands in the evaluation scripts.

#### Hypernym Discovery

Coming soon!

### Reference paper

If you use any of these resources, please cite the following [paper](https://arxiv.org/abs/1808.08780):
```bash
@InProceedings{doval:meemiemnlp2018,
  author = 	"Doval, Yerai and Camacho-Collados, Jose and Espinosa-Anke, Luis and Schockaert, Steven",
  title = 	"Improving cross-lingual word embeddings by meeting in the middle",
  booktitle = 	"Proceedings of EMNLP",
  year = 	"2018",
  publisher = 	"Association for Computational Linguistics",
  location = 	"Brussels, Belgium"
}

```

If you use VecMap or MUSE, please also cite their corresponding papers.
