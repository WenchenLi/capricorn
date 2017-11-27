# NLP vocab
NLP vocab is a lightweight library for helping prepare vocabulary from 
corpus and prepare word embedding ready to be used by learning models.

To be more specifically, it helps:
1. build vocabulary from corpus
2. load necessary word embedding with consistent word index in Vocabulary

# getting started
```python
import nlp_vocab


Vocab_path = "vocab_processor"
embedding_vector_path = "data/embedding/model.vec"

# Load vocab
if os.path.isfile(Vocab_path):
	print("Loading Vocabulary ...")
	vocab_processor = nlp_vocab.VocabularyProcessor.restore(Vocab_path)

else: # build vocab
	print("Building Vocabulary ...")
	
	x_text = ["Saudi Arabia Equity Movers: Almarai, Jarir Marketing and Spimaco.",
                        "Orange, Thales to Get French Cloud Computing Funds, Figaro Says.",
                        "Stansted Could Double Passengers on Deregulation, Times Reports."]

	# Build/load vocabulary
	max_document_length = 11
	min_freq_filter = 2

	vocab_processor = nlp_vocab.VocabularyProcessor(max_document_length, min_frequency=min_freq_filter)
	vocab_processor.fit(x_text)
	vocab_processor.save(Vocab_path)
	print "vocab_processor saved at:", Vocab_path

# build embedding matrix of which the index is consistent with vocab word2index mapping	
embedding_matrix = vocab_processor.prepare_embedding_matrix(embedding_vector_path)

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

## Support language [under development]

Currently focus on support English and Chinese,
these two type can be later generalized to language pipeline
whether needs words segmentation.   