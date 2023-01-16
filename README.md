# PT_QA_Agents

This repository includes the implementations of several alternatives to the creation of conversational agents, fully configured to receive either a list of FAQs or a collection of plain text documents and answer questions related to the given domain, in Portuguese.

The alternatives include an NLU platform, Google Dialogflow, an IR-based approach, text search engine Whoosh, two types of state-of-the-art transformer-based language models, namely BERT and answer-generating GPT-2, and Google's Multilingual Universal Sentence Encoder trained for QA.
For every alternative there is at least one configuration, with each configuration being implemented in a different Google Colab notebook.

All configurations receive as input two files: 
* a file containing the domain (a list of FAQs or a collection of plain text documents);
* a file containing a list of questions.

All configurations retrieve one single file:
* a plain text file containing all the posed questions and corresponding obtained answers, identified by a 'P: ' and a 'R: ', respectively.

The Colab notebooks are as follows:

* **Dialogflow_Intents** - Google Dialogflow agent that creates an intent per question-answer pair and retrieves answers through the Dialogflow API.
*Implemented for FAQs.*

* **Dialogflow_KB** - Google Dialogflow agent that creates a knowledge base with either a list of FAQs or a collection of plain text documents and retrieves answers through the Dialogflow API.
*Implemented for FAQs and Text.*

* **Whoosh_Ques_Ans_Search** - Whoosh engine that creates a document per question-answer pair and searches for the document containing either the most similar question or both the most similar question and answer to the posed question. 
Retrieves the answer in that same document.
*Implemented for FAQs.*

* **Whoosh_Highlights** - Whoosh engine that, in a collection of plain text documents, searches the document most similar to the posed question and retrieves as an answer the spans of text from that same document deemed as most similar to the question.
*Implemented for Text.*

* **BERT_NLI** - Portuguese-cased BERT model that computes the vector representations of each question-answer pair and the posed question, making use of Natural Language Inference. The similarity is then calculated between the question and each pair.
Returns the answer corresponding to the pair with the most similar representation to the posed question.
*Implemented for FAQs.* 

* **BERT_FE** - Portuguese-cased BERT model that computes the vector representations of each question-answer pair and the posed question. The similarity is then calculated between the question and each pair.
Returns the answer corresponding to the pair with the most similar representation to the posed question.
*Implemented for FAQs.*

* **BERT_Clustering** - Portuguese-cased BERT model that computes the vector representations of each question-answer pair and the posed question. A k-means clustering of the pairs is then performed.
The similarity between the centroid of each cluster and the posed question is calculated, and the cluster deemed as most similar is used as context in Portuguese-cased BERT-QA, which retrieves a span of text from the context as an answer.
*Implemented for FAQs.*

* **BERT_Whoosh** - Combination of search engine Whoosh and Portuguese-cased BERT model.
Whoosh pre-selects the most similar document, from a collection of plain text documents, to the posed question.
The document deemed as most similar is then used as context in Portuguese-cased BERT-QA, which retrieves a span of text from the context as an answer.
*Implemented for Text.*

* **GPT2** - GPT-2 model that is finetuned on either a list of FAQs or a collection of plain text documents and generates answers based on the domain in which it was finetuned. 
*Implemented for FAQs and Text.*

* **USE-QA** - Universal Sentence Encoder Q&A Retrieval model that computes the vector representations of a list of sentence-context pairs, with the context being the text surrounding the sentence. We define the sentence as the question from a question-answer pair and the respective context as the whole pair. Such representations are then stored in a simpleneighbors index. Upon receiving a question, USE-QA computes its vector representation, later used to query the previously created index.
This index then returns an ordered list of of approximate nearest neighbors in semantic space, from which we retrieve the answer.
*Implemented for FAQs.*

To test the different implementations, two datasets are also included in this repository. One contains a list of FAQs and the other a collection of plain text documents.

# How to cite

<pre>
@inproceedings{goncalo-oliveira_etal:slate2022,
	address = {Dagstuhl, Germany},
	author = {Gon\c{c}alo Oliveira, Hugo and In\'{a}cio, Sara and Silva, Catarina},
	booktitle = {Proceedings of 11th Symposium on Languages, Applications and Technologies (SLATE 2022)},
	editor = {Cordeiro, Jo\~{a}o and Pereira, Maria Jo\~{a}o and Rodrigues, Nuno F. and Pais, Sebasti\~{a}o},
	pages = {19:1--19:11},
	publisher = {Schloss Dagstuhl -- Leibniz-Zentrum f{\"u}r Informatik},
	series = {Open Access Series in Informatics (OASIcs)},
	title = {{Analysing Off-The-Shelf Options for Question Answering with Portuguese FAQs}},
	volume = {104},
	year = {2022}}
</pre>
