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

## **Description of the notebooks**

The development of this study has employed the datasets provided by Cantemist. [3] The collection of files employed include train, development 1, development 2, test and background, and test with gold standard files. 

The execution of the notebooks should be performed in the following order:

**1. Preprocessing_NER**

The aim of this notebook is to read the text and annotation files regarding each dataset and perform some preprocessing steps to combine the information of the txt and ann files into a single dataframe. 

**2. NER_by_CRF**

The output of this notebook is the predictions of the test and background files stored in various arrays;"new_tokens_cc", "new_start_pos_cc" and "new_labels_cc". These arrays contain the necessary information to construct the annotations in BRAT format for every clinical case.

**3. NER_by_BILSTM_CRF**

The output of this notebook is the predictions of the test and background files stored in various arrays;"new_tokens_cc", "new_start_pos_cc" and "new_labels_cc". These arrays contain the necessary information to construct the annotations in BRAT format for every clinical case.

**4. NER_by_BERT**

The output of this notebook is the predictions of the test and background files stored in various arrays;"new_tokens_cc", "new_start_pos_cc" and "new_labels_cc". These arrays contain the necessary information to construct the annotations in BRAT format for every clinical case.

**5. Create_ann_files**

This notebook constructs the annotation files of the test and background dataset employing the predictions of the previous notebooks. Therefore, there is a single code regardless of the method. The only concern is to read the predictions of just one method at a time and execute the code to construct the annotations. Then, these annotations are stored in independent .ann files based on the clinical case. Therefore, considering just one method, for instance, NER_by CRF, the code will store as many .ann files as clinical cases.

**6. Check_entity_match**

The annotation files were constructed for a collection of files that included both test and background clinical cases. The true annotation files of this dataset were unknown However, the performance of the final models is just evaluated over the test files, for which the test with gold standards files were released later on. In order to identify which files in the test and background dataset matched the one in the test with gold standards, the file names were employed. 

****

## References

[1] Soares, F., Villegas, M., Gonzalez-Agirre, A., Krallinger, M., & Armengol-Estapé, J. (2019, June). Medical word embeddings for Spanish: Development and evaluation. In Proceedings of the 2nd Clinical Natural Language Processing Workshop (pp. 124-133).

[2] DEVLIN, Jacob, et al. Bert: Pre-training of deep bidirectional transformers for language understanding. arXiv preprint arXiv:1810.04805, 2018

[3] A. Miranda-Escalada, E. Farré, M. Krallinger, Named entity recognition, concept normal- ization and clinical coding: Overview of the cantemist track for cancer text mining in spanish, corpus, guidelines, methods and results, in: Proceedings of the Iberian Languages Evaluation Forum (IberLEF 2020), CEUR Workshop Proceedings, 2020.
