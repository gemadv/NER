# NER


## **Description of the systems:**

The output predictions (named entities) of the following systems have been computed for every clinical case independently.

**1-CRF**

This system consists on implementing a CRF, Conditional Random Field, over the preprocessed inputs. For this purpose, the system employs a representation of each word in the clinical cases formed by such word or token, its part of speech tag,the previous and next words and their corresponding PoS tags. The PoS tags have been obtained through spaCy.


**2-BILSTM-CRF**

*2.1-Approach 1: BILSTM-CRF with random initialization of vectors*

This approach consists on implementing a bidirectional LSTM (Long Short-Term Memory), which is a type of Recursive Neural Network, followed by a Conditional Random Field. This system's input is a representation of every token in the sentences (of fixed length) of the corpus as a numeric vector. Moreover, it considers a random initialization of the vectors for the word embedding. 

*2.2-Approach 2: BILSTM-CRF with a pre-trained word embedding in Spanish*

This approach also consists on implementing a bidirectional LSTM (Long Short-Term Memory) network followed by a Conditional Random Field. Nevertheless, it is different from the previous approach since it employs a pre-trained word embedding in Spanish. More specifically, it implements the Scielo + Wikipedia health cased skip-gram model. [1] Here, every token in the sentences that conform the corpus is converted into a 300-element vector using the pretrained word embedding as a vocabulary.  

*2.3-Approach 3: BILSTM-CRF with character embedding*

This approach also consists on implementing a bidirectional LSTM (Long Short-Term Memory) network followed by a Conditional Random Field. Similarly as in 3-systemBILSTM2, it implements the Scielo + Wikipedia health cased skip-gram model [1] as a pre-trained word embedding to construct the feature representation. However, this system also employs character embedding concatenated with the word embedding, as an input. 

**3-BERT**

This system employs an already pre-trained BERT model, Bidirectional Encoder Representations from Transformers, proposed by Jacob Devlin, Ming-Wei Chang, Kenton Lee and Kristina Toutanova. [2] Given the fact that this task involves working with clinical cases in Spanish, the multilingual cased version of BERT has been used. This strategy allows to consider information from both directions without the need to employ two independent LSTMs, as in the previous systems. 

****

## References

[1] Soares, F., Villegas, M., Gonzalez-Agirre, A., Krallinger, M., & Armengol-Estapé, J. (2019, June). Medical word embeddings for Spanish: Development and evaluation. In Proceedings of the 2nd Clinical Natural Language Processing Workshop (pp. 124-133).

[2] DEVLIN, Jacob, et al. Bert: Pre-training of deep bidirectional transformers for language understanding. arXiv preprint arXiv:1810.04805, 2018
