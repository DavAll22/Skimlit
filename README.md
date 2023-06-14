# Skimlit

Project replicating the NLP deep learning model used to classify sentences which appear in sequential order within a scientific report abstract (https://arxiv.org/abs/1710.06071) in order to read the key infromation faster. The aim for this NLP model is to learn and classify sentences into the report structure categories. NLP text vectorization and emnbedding methods are used, including concatenation of character-level and token embeddings, as well as feature engineering.

# This project uses:
* TensorFlow 2.X to create, train and evaluate the performance of NLP embedding methods [Token embedding, Character-level embedding, Feature Engineering]
* Functional API to build the models, tf.data API to build and zip the datasets
* Label-encoded labels cor class names
* Dropout layers to reduce overfitting
* Using spaCy to enter text into the model

The dataset used is called PubMed 200k RCT - 200,000 abstracts of randomised controlled trials (RCT) totalling 2.3 million sentences. Each sentence is labelled with their role in the abstract (https://github.com/Franck-Dernoncourt/pubmed-rct.git). The 20k dataset with the numbers replaced with @ symbols has been used for this project to help speed up training times and keep experiments shorter. Batches of 10% of this size are used for training and validation and evaluated on the whole validation dataset.

The abstracts are pre-processed and split into sentences for each of the train, validation and test sets, with 180k training samples, 30k validation samples and 30k test samples (75:12.5:12.5). Validation occurs simultaneously when taining the model.

The models used and compared are:

0. Baseline model - TF-IDF score with Multinomial Naive Bayes
1. Conv1D with custom Token Embedding
2. Transfer Learning with pre-trained embedding layer (Universal Sentence Encoder)
3. Conv1D with Character-Level Embedding
4. Bi-Directional LSTM and Hybrid Embedding Layer (concatenation of token and character embeddings)
5. Feature Engineering (Adding sentence position embedding and concatenating with the hybrid embedding)

![image](https://github.com/DavAll22/Skimlit/assets/124359152/e2cbf77a-0b85-4e99-9b3c-a12b3f6cac1c)

# Evaluation

![image](https://github.com/DavAll22/Skimlit/assets/124359152/9ba25358-f316-429d-98fd-75169925406e)

The model using the Tribrid method of concatenating position, token and character embeddings resulted in the highest accuracies overall. 
However it is found that the model struggles to predict accurately on sentences which are ambiguous in terms of their content (i.e. the sentence can belong in multiple classes, such as Background and Objective) which can be seen in the confusion matrix and the top 100 most wrong predictions.

![image](https://github.com/DavAll22/Skimlit/assets/124359152/22b6d067-afad-4542-9e2d-c7f16cabedf3)

Entering abstracts into the model using spaCy results in the sentences being divided into their respective labels and achieves the task set out for the project in replicating the paper's model.
