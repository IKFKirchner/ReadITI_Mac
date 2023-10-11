# What is ReadITI_Mac?

ReadITI_Mac is an adaption of ReadITI (https://github.com/Maroussia/readiti) by Dr. Maroussia B. with some minor changes by me to adapt it for Mac users. These changes address the fact that hidden files in Macbook folders frequently disrupt the proper functioning of code and, in this case, do not allow for ReadITI to run on a folder of .txt files. Specifically, I modified the dir_processor function to handle files more robustly so that it now checks whether each file is a valid text file before attempting to process it. It uses the os.path.isfile function to determine if a file exists and is not a directory, and then check its extension to ensure it's a .txt file. 

# On ReadITI

ReadITI is designed to prepare texts from the OpenITI corpus for Natural Language Processing (NLP).
You can download OpenITI at [Zenodo](https://doi.org/10.5281/zenodo.6808108). If you use it, be sure to cite

 > Nigst, Lorenz, Romanov, Maxim, Savant, Sarah Bowen, Seydi, Masoumeh, & Verkinderen, Peter. (2022). OpenITI: a Machine-Readable Corpus of Islamicate Texts (2022.1.6) [Data set]. Zenodo. 


ReadITI is inspired from [`openiti.helper.ara`](
https://openiti.readthedocs.io/en/latest/source/usermanual.html#openiti-helper).

ReadITI (1) separates the metadata from the main text and (2) cuts the text into sentences or paragraphs using the OpenITI hashtags (`#`), whereas `openiti.helper.ara.tokenize` preserves metadata so that it will appear in your tokenized input, which is not what you want for NLP.

# Installation

You can install `ReadITI` in your local environment using the following steps (after activating your environement):
```
git clone git@github.com/Maroussia/readiti.git
```
```
cd readiti
```
```
pip install -e .
```
You can also download only `readiti/readiti/readiti.py` or use the Jupyter Notebook `readiti/readiti_for_trials.ipynb`.

# Using ReadITI

The function `readiti.file_processor` processes single files and is meant for scholars working with one version of a given text.

The function `readiti.dir_preprocessor` processes all the files in a directory and is addressed to scholars who have extracted a corpus with multiple texts. Set `verbose=False` to prevent the printing of statistics during preprocessing.

The **input** for both functions should be raw files from OpenITI.

The **output** for both functions consists of 3 files per input file. Output file names are the original OpenITI name `<name>` with a suffix:

1. a `<name>.txt_tokens.txt` file containing one *token* per line resulting from simple white-space tokenization.
	
2. a `<name>.txt_sentences.txt` file containing one OpenITI *sentence* per line. The end of a sentence corresponds to a new line in the original text, which OpenITI marks with a hastag (`#`). Hence you can cut up sentences in the input by inserting `#` at the desired sites.
	
3. a `<name>.txt_doc.tsv` table where the tab (`\t`)-separated columns contain: 


	| idx | token | start_char | end_char|

i.e. token id (index into the vocabulary), token characters, index of the starting character, index of ending character.

Sentences in output files are separated by two new lines (`\n\n`).

See the folder `readiti/data/trial_with_folder/output` for examples.

# Feedback

Anything missing? Do get in touch or open up a pull request :).
