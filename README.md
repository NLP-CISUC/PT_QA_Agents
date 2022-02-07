# PT_QA_Agents

This repository includes the implementations of several alternatives to the creation of conversational agents, fully configured to receive either a list of FAQs or a collection of plain text documents and answer questions related to the given domain, in Portuguese.

The alternatives include an NLU platform, Google Dialogflow, an IR-based approach, text search engine Whoosh, and two types of state-of-the-art transformer-based language models, namely BERT and answer-generating GPT-2.
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

* **Whoosh_Ques_Search** - Whoosh engine that creates a document per question-answer pair and searches for the document containing the question most similar to the posed one, and retrieves the answer in that same document.
*Implemented for FAQs.*

* **Whoosh_Ques_Ans_Search** - Whoosh engine that creates a document per question-answer pair and searches for the document containing both the question and answer most similar to the posed question, and retrieves the answer in that same document.
*Implemented for FAQs.*

* **Whoosh_Highlights** - Whoosh engine that, in a collection of plain text documents, searches the document most similar to the posed question and retrieves as an answer the spans of text from that same document deemed as most similar to the question.
*Implemented for Text.*

* **BERT_FE** - BERT model that computes the vector representations of each question-answer pair and the posed question, and calculates the similarity between the question and each pair.
Returns the answer corresponding to the pair with the most similar representation to the posed question.
*Implemented for FAQs.*

* **BERT_Clustering** - BERT model that computes the vector representations of each question-answer pair and the posed question, and performs a k-means clustering of the pairs.
Then calculates the similarity between the centroid of each cluster and the posed question.
The cluster deemed as most similar is used as context in BERT-QA, which retrieves a span of text from the context as an answer.
*Implemented for FAQs.*

* **BERT_Whoosh** - Combination of search engine Whoosh and BERT model.
Whoosh pre-selects the most similar document, from a collection of plain text documents, to the posed question.
The document deemed as most similar is then used as context in BERT-QA, which retrieves a span of text from the context as an answer.
*Implemented for Text.*

* **GPT2** - GPT-2 model that is finetuned on either a list of FAQs or a collection of plain text documents and generates answers based on the domain in which it was finetuned. 
*Implemented for FAQs and Text.*
