#SULI Project
#Application of Natural Language Processing on Elogs
Dale Yu, Computer Science Technologies, Columbia University, Setauket, NY, 11733
Mentor: Prerana Kankiya, Controls Team, Brookhaven National Laboratory, Upton, NY 11973

#### Description: 
At the various particle accelerators like the Relativistic Heavy Ion Collider (RHIC) at Brookhaven National Laboratory, the machines are constantly monitored, and data is recorded by the set of experts on site. During each run, the operators and system experts enter free formatted notes into an electronic logbook. These electronic logbooks are stored on a large database with millions of entries that could contain anything from general operations to major observations as well as events of failures. Though an elog search facility is supported, it can at times be difficult to find information in the elogs.  Our research project plans to build an algorithm that can classify text from elog entries and assign tags in order to facilitate filtering and searching.  In addition, the project plans to investigate common trends and patterns used, in order to create summary reports. 

#### Why?:
Machine learning technologies enable large data correlation and simplify complex computational tasks, so gaining more experience in this field is likely to provide efficient tools for conducting research at the collider accelerator department and various DOE projects. 

## Content
1. Data Collection
    * What is an E-Log
    * Reading From the E-Logs
    <br/><br/>
2. <u>**Text Processing**</u>
    * Tokenizing
    * Stop Words
    * Lemmanizing 
    * Final Preprocessing
    <br/><br/>
3. Word Representation
    * Word Cloud
<br/><br/>
4. <u>**SKLearn Count Vectorizer**</u>
    * Load and Split Training Data
    * Balancing Training Data
    * Creating the Vector Space Model
    * Naive Bayes Classification
<br/><br/>
5. TF-IDF Transformation (term frequency-inverse document frequency)
    * Count Vectorizer -> TF-IDF
    * Naive Bayes Classification
<br/><br/>
6. Confusion Matrix and Validating Classifier
    * Classification Results
<br/><br/>
7. <u>**Word2Vec Model**</u>
    * Bigram Phrases
    * Create Word2Vec Skip Gram Model
    * Word2Vec Embeddings
<br/><br/>
8. Keras Neural Network
    * Word2Vec embedding layer
<br/><br/>
9. K-Means Clustering of Word2Vec
    * Silhouette Test
    * Dimensional Reduction of Word2Vec Vectorized Representation
        * t-SNE Dimensional Reduction
        * PCA Dimensional Reduction
    * Cluster Word2Vec using NLTK KMeans Clusterer
    * 2-Dimensional Cluster Representation
    * 3-Dimensional Cluster Representation
<br/><br/>
10. <u>**Doc2Vec Model**</u>    
    * Create Tagged Documents
    * Building Model
    * Finding Similar E-Logs
<br/><br/>
11. K-Means Clustering of Doc2Vec 
    * Analysis of Clusters using WCSS and BCSS
    * Silhouette Test
    * Dimensional Reduction of Doc2Vec Vectorized Representation
    * 2-Dimensional Cluster Representation
    * 3-Dimensional Cluster Representation


### Data Collection
<u>What is an E-log?</u> <br></br>
    An E-Log is a free formatted log journal that operators and system experts enter information and notes into during each run. These logbooks can be both automated and manually entered and there are millions of entries with new ones added every few minutes. In this large database, there is a lot of information to be loaded and analyzed, so using natural language processing and machine learning can help us understand the contents and find interesting information.  
<br></br>
Some of the Goals of Reading these elogs are to: <br></br>
    1. Classify <br></br>
    2. Find trends<br></br>
    3. Create Summaries<br></br>

Before any of this is possible, it is important to look at the database and how to retrieve information from it. For this project, information was received from only the years of 2022 and 2021. 2022 was mostly used as it was a major run for the particle accelerator, but entries from 2021 were also used to help create a bigger set for the classifier. 

<u>Reading From an Elog</u>
<br></br>
The log entries are saved into a MySQL database, so I had to use a MySQL query and an in python mysql Connector cursor to get the data that I needed. Below you can see the queries that were used to get the two training data sets, RHIC elog set, and testing set for tagging. <br></br>
All the logs were loaded into a JSON file format because Pandas and python have a built-in and easy way to parse through and filter through JSON files. It is also a fast text file to read through in the case that the project might get scaled up to be used against more entries than it currently is. The MySQL entries used the JSON_OBJECT function to load all the data into the proper format to be parse and separated. There were some difficulties with this at first, but after some tinkering it was able to load with the data that I needed for the project. I selected the fields of ID, Content, Machine, and the Timestamp. There are many more fields to the dataframe, but I found these to be the most important ones, so I only selected them. There were also errors with the processing later on, so this resulted in changes being made like reducing all null Content entries and separating the tagged from the untagged. This was to reduce the chances of overfitting and create a better classification model. 