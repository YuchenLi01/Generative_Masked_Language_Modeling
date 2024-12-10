# **Pa**rallel **D**ecoding by **I**terative **R**efinement
This repo contains the authors' implementation of the ICML 2024 paper
[Promises and Pitfalls of Generative Masked Language Modeling: Theoretical Framework and Practical Guidelines](https://arxiv.org/abs/2407.21046),
and is forked from [this public Google Research repo](https://github.com/google-research/google-research/tree/master/padir).

PaDIR (**Pa**rallel **D**ecoding by **I**terative **R**efinement) is a
non-autoregressive decoder implementation in Jax. It builds on top of the T5X
framework, for which documentation is available
[here](https://github.com/google-research/t5x).

Please note that this codebase is experimental.

## Vocabulary

The [MT5](https://github.com/google-research/multilingual-t5) multilingual
vocabulary (256k tokens) is used by default.

In our paper, we use custom bilingual vocabularies.
These can be created as follows:

* Run the `padir/vocab/extract_features.py` script for the desired
[TFDS](https://www.tensorflow.org/datasets) dataset (e.g., WMT14 EN-DE).

* Create a [sentence-piece](https://github.com/google/sentencepiece) vocabulary
using the data extracted in the previous step.
For our experiments we run the sentence-piece training script with the
following parameters:
```--vocab_size=32000 --max_sentence_length=100000 --pad_id=0 --eos_id=1 --unk_id=2 --bos_id=3```.

* Update the _CUSTOM_VOCAB_FILE variable inside `padir/config_options.py`
and update the PaDIR config accordingly, before training your model.

## Dataset

Distilled datasets in our paper were created via the Google Cloud Translate API.
Reducing noise in the data helps train significantly better models.
We are not able to release these datasets but similar datasets can be
recreated with any Translation API or most large language models.

## Citation

If you use or extend this work, please cite our paper as follows:

```
@inproceedings{li2024promises,
    author = {Yuchen Li and Alexandre Kirchmeyer and Aashay Mehta and Yilong Qin and Boris Dadachev and Kishore Papineni and Sanjiv Kumar and Andrej Risteski},
    title = {Promises and Pitfalls of Generative Masked Language Modeling: Theoretical Framework and Practical Guidelines},
    year = {2024},
    publisher = {JMLR.org},
    booktitle = {Forty-first International Conference on Machine Learning},
    series = {ICML'24}
}
```

## Note

This is not an officially supported Google product.
