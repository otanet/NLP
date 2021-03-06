# NLP - Unstructured Text to Knowledge graph conversion
1.    Dataset Folder:
a.    Ner_dataset.csv - is a GMB corpus which is an annotated Kaggle dataset used for performance comparison between CRF and Spacy for NER
b.    ActorsDataset folder - Consists of the list of 25 actors text file that contains the wikipedia scraped data using “wikipedia_web_parser.ipynb”. These files contain the unstructured text used for processing and building the knowledge graph. 
c.    ActorsPreprocessedDataset - This contains the co-reference resolved text data corresponding the previous unstructured text data present in the ActorsDataset. This dataset is generated by Stanford-CoreNLP (execution is explained below).

2.    Code Execution:
a.    Prerequisite:
i.    Install the following packages Beautiful Soup, unidecode, sklearn_crfsuite, Pandas, NLTK, Spacy, Textacy, Neo4j, Py2neo
ii.    Download and install Neo4j: For Instructions follow: https://neo4j.com/download/
Commands:

pip install beautifulsoup4
sudo pip install pexpect unidecode
pip install sklearn_crfsuite
Install: pip install pandas
pip install -U nltk
import nltk
nltk.download('punkt')
nltk.download('averaged_perceptron_tagger')
pip install spacy
pip install textacy
pip install pickle
pip install py2neo

b.    Execution:
i.    The “Code” folder contains all the scripts that were used to generate the dataset and the knowledge graph. 
1.    The “htlm_jupyter_notebook” folder contains all the respective .html files corresponding to the “.ipynb” jupyter notebook as mentioned below.

2.    Wikipedia_web_parser.ipynb - Web scraper script used to extract unstructured American actor text data from Wikipedia. The script has been already run and the text files generated are placed in the “Dataset/ActorsDataset”. [Not required to run this file again]
3.    NER_CRF_Spacy_Comparison.ipynb - This file consists of the performance comparison between CRF and Spacy for NER using annotated dataset. This file can be executed for running all the cells in the jupyter notebook following the instructions mentioned inside the notebook. To execute this code, place the ner_dataset.csv file in the same directory location as this .ipynb file [Not required but can execute this file to see the results]
4.    stanford-corenlp-python: This folder contains the necessary resources to do coreference resolution on the input text that we provide. Follow the below instructions to do the same
a.    Install pexpect unicode: sudo pip install pexpect unidecode
b.    cd stanford-corenlp-python
c.    Run the file to start the RPC server: python corenlp.py
d.    Install pandas: pip install pandas
e.    pip install -U nltk
f.    Open python shell and run the commands g-i.
g.    import nltk
h.    nltk.download('punkt')
i.    nltk.download('averaged_perceptron_tagger')
j.    Create  a directory called ActorsPreprocessedDataset in this folder.
k.    Run the file python coref.py
This will generate the pre-processed text files that are saved in the
ActorsPreprocessedDataset folder.                          
5.    NER_RE.ipynb: This file is responsible for reading our pre-processed files and performingNamed Entity Recognition and Relationship Extraction. It saves the entities dictionary and also the the Subject Verb Objects extracted as svos.csv 
Install the below packages before executing all the cells :
pip install spacy
pip install textacy
pip install pickle
6.    query_interface_and_google_KG_comparison.ipynb: this file provides the knowledge graph construction and menu driven query interfacing. To execute the file follow the below instructions
a.    Install and start a graph instance in Neo4j application
b.    Update the connection link inside the notebook with the respective password .
graph = Graph("bolt://localhost:7687",password=”<your password>")
c.     Run all the cells and the user interactive MENU gets displayed. 
Menu 
--------

1. Get names of all actors
2. Get names of all producers
3. Get names of all multi-talented people
4. Get description of a specific person
5. Get all node relations present in KG
0. Exit
Enter choice (0 to 5): 1
Provide the required option to view the query result from the knowledge graph. Valid inputs are within (0 to 5)
d.    The later part of the notebook provides the comparison between the response of our algorithm query and the Google Knowledge graph API query response for a particular person name. To execute this, update the API_KEY with your access api key for Google Knowledge Graph API 

Find the project features: https://www.youtube.com/watch?v=jOugBeAST_Q&t=283s

References:
1.    Stanford-CoreNLP : https://github.com/dasmith/stanford-corenlp-python
2.    Coreference Resolution: https://github.com/aleenaraj/Coreference_Resolution

