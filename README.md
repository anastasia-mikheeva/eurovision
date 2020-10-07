# A Deep Learning model to write a new Eurovision Entry
Final Project for Spiced Academy Data Science Bootcamp (born as a joke during lockdown).

This project was completed in [Google Colab](https://colab.research.google.com/) on GPU runtime.

## Credits
This project uses the [Eurovision Dataset](https://github.com/Spijkervet/eurovision-dataset) by [Janne Spijkervet](https://github.com/Spijkervet).

It is an adaptation of the Text Generation model in [this Medium article](https://towardsdatascience.com/generating-indonesian-lyric-using-deep-learning-first-part-2c7634237475) by [Haryo Akbarianto Wibowo](https://towardsdatascience.com/@haryoaw).

It uses pre-trained vectors from [GloVe: Global Vectors for Word Representation (2014)
](https://nlp.stanford.edu/pubs/glove.pdf) by Jeffrey Pennington, Richard Socher, and Christopher D. Manning, as well as a custom sequential Attention layer by github user [@iridiumblue](https://github.com/iridiumblue).

A huge thank you to all the teachers at [Spiced Academy](https://github.com/spicedacademy) for their help and support!

## Installation Instructions
In order to run the Colab Notebook, the following prerequisites are required:
  - The custom [Attention Layer for Keras](https://gist.github.com/iridiumblue/622a9525189d48e9c00659fea269bfa4) by github user [@iridiumblue](https://github.com/iridiumblue) must be in the parent directory. It can be uploaded to the temporary folder in Colab to run the code. Otherwise a different filepath must be specified.
  - The GloVe pretrained vectors must be uploaded to the Colab temporary directory. The notebook uses the 100d 6B vectors. The filepath must be changed accordingly if linking to a different/permanent location.
  - A pip installable **requirements.txt** file has been provided.
  - There is a separate corpus which has been tokenized and filtered for English line-by-line and then word-by-word. This is in the file **corpus** and must also be in the parent directory. The Tokenizer object is also provided in the **tokenizer** file. (See language notes below). The separation and language detection line by line takes several hours to run from scratch, so I recommend using the preprocessed data. Otherwise the separation script is available as **language_cleaning.ipynb**

## Modifications to the code
- The model was trained on sentences of length 15. In order to change this, the variable `WINDOW` must be changed to the required value.
- If using GloVe vectors of higher dimensions than 100, the variable `EMBEDDING_DIMS` must be changed accordingly.

## Notes about Language
In the original dataset, no information about the language of each song was provided. Since some songs are written in a mixture of different languages, and the lyrics in languages not using cyrillic script are provided in transliterated form, a particular challenge of this project was to provide a "clean" English vocabulary for the model to train on. The final solution was to separate the songs into substrings line by line, run these through [GoogleTrans](https://pypi.org/project/googletrans/) language detection, and then tokenize into words which were individually compared with the [enchant](https://pypi.org/project/pyenchant/) US English dictionary. Some songs and words in French, Dutch and other languages were still classfied as English by google translate, and some single words present in English in some contexts made it into the final vocabulary from non-English songs. There is scope for improvement on this issue.
