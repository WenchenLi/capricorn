
<div align="center">
  <img src="img_src/Capricorn_icon_sml.png"><br><br>
</div>

-----------------

# capricorn

capricorn is a lightweight library for helping prepare vocabulary from
corpus and prepare word embedding ready to be used by learning models.

1. build vocabulary from corpus
2. load necessary word embedding with consistent word index in Vocabulary


## getting started
```
pip install capricorn
```

```python
import capricorn
import os

# Specify filepaths
Vocab_path = "vocab_processor"
embedding_vector_path = "path/to/embedding"

# Load vocab
if os.path.isfile(Vocab_path):
  print("Loading Vocabulary ...")
  vocab_processor = capricorn.VocabularyProcessor.restore(Vocab_path)

else:  # build vocab
  print("Building Vocabulary ...")

  x_text = ["Saudi Arabia Equity Movers: Almarai, Jarir Marketing and Spimaco.",
            "Orange, Thales to Get French Cloud Computing Funds, Figaro Says.",
            "Stansted Could Double Passengers on Deregulation, Times Reports."]

  # Build/load vocabulary
  max_document_length = 11
  min_freq_filter = 2

  vocab_processor = capricorn.VocabularyProcessor(max_document_length=max_document_length,
                                                  min_frequency=min_freq_filter)
  # only fit
  # vocab_processor.fit(x_text)
  # or fit_transform to get the transformed corpus
  x_text_transformed = vocab_processor.fit_transform(x_text)
  vocab_processor.save(Vocab_path)
  print("vocab_processor saved at:", Vocab_path)

# build embedding matrix of which the index is consistent with vocab word2index mapping
embedding_matrix = vocab_processor.prepare_embedding_matrix_with_dim(embedding_vector_path, 300)

```
# User input

The library default to use special token \_\_UNK__  and \_\_PAD__, 
if the input sequence lengths below the max_document_length when initial
VocabularyProcessor, it will automatically pad the sequence use the \_\_PAD__. 

    
If user have pre defined special tokens when initialize Vocabulary, user 
need to pre-process the sequence, namely adding the self defined special 
tokens to the input sequence. For example if user defined \_\_START__
and \_\_END__ as additional special tokens and max_document_length=11,  User has to process the original
sentence from: 

"We like it very much" 

to:

"\_\_START__ \_\_PAD__ \_\_PAD__  We like it very much \_\_PAD__ \_\_PAD__ \_\_END__"
