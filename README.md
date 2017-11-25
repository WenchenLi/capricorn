# NLP vocab
NLP vocab is a lightweight library for helping prepare vocabulary from 
corpus and prepare word embedding ready to be used by learning models.

To be more specifically, it helps:
1. build vocabulary from corpus
2. load necessary word embedding with consistent word index in Vocabulary

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

## Support language

Currently focus on support English and Chinese,
these two type can be later generalized to language pipeline
whether needs words segmentation.   