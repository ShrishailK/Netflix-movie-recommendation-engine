# Netflix-content-recommendation-engine

### Table of Content:

1. [Project Motivation](#motivation)
2. [Descriptions](#file)
3. [Installation](#installation) 
4. [Results and Improvements](#results)
   
## Project Motivation : <a name="motivation"></a>
Building an unsupervised content based recommendation engine. We want to build a recommendation engine that recommends users of Netflix similar content to one they are currently browsing using text features of all the given movies. 

What are we intereseted in answering the following question:
1. What content is similar to current content being browsed by the user?


## Descriptions : <a name="file"></a>
The dataset `netflix_titles.csv` used in this notebook contains real Netflix app content data.

Here is the explanation of each pertinent feature in the file :
   - title : The title or name of the given movie / tv series
   - country : The country with which the content is associated
   - director : The name of the director of the movie / tv series
   - cast : The name of the actors in the movie / tv series
   - listed_in : The genre and other categories under which a movie / tv series is listed
   - description : The description of the story movie / tv series

Program Flow:

![image](https://user-images.githubusercontent.com/75063039/127771179-b96f8ee4-2104-4837-94ed-32a425c7b6bf.png)

Check results present in the Netflix recommendation engine notebook.

Notebook descriptions:
 - ETL Notebook : This notebook contains the implemented Extract, Transform and load pipline (ETL pipeline). The ETL notebook contains a class defined as ETL which does the following:
    -  Stores a dataset named df which contains description and listed_in column for each movie to be used later in better understanding of results. 
    -  Cleans the stopwords and lowers the entire text case in description column before converting  into a list for each movie stored in description column of that movie.
    -  Joins the first and the last name and lower the text case in director column before converting into a list for each movie stored in director column of that movie.
    -  Joins the first and last name of the cast names, lowers the text case and removes the ',' to form a list of top three cast names for each movie stored in cast column of that movie.
    -  Joins the words in country column name, lowers it and converts into a list for each movie stored in country column of that movie.
    -  Removes the ',' from listed_in and converts it into an list of words for each movie and stored in listed_in column of that movie
    -  Last step joins all the columns present in the form of lists for each movie, converts it into a string and stores it in new column named 'text' for that movie.
    -  The text and title column are kept for each movie and the rest of the columns are deleted. The text column is now in proper processed form to implement the machine learning pipeline on it to get results.
    -  The class also creates a dataset 
 - Modelling Notebook : This notebook contains the Machine learning pipeline developed with NLTK and Scikit-Learn. (The class defined as results of this pipeline are well defined in the code and do not need an explanation)
 - Visualization : This notebook contains functions used in result class of the Machine learning pipeline(Modelling notebook) for result visualization.
 - Amazon recommendation engine : Run this notebook to implement the above pipelines and see the results.


## Installation : <a name="installation"></a>
  - Gensim 4.0.1 for using pretrained word2vec library by Google.
  - Cython 0.29.21 for using pretrained word2vec library by Google.
  - Matplotlib version 3.2.0 for heatmaps.
  - Python version  3.*.


## Results and Improvements: <a name="results"></a>

### Results : 

The main findings of this project can be found in my medium post [here](https://shrishailkandi95.medium.com/content-based-movie-recommendation-system-for-netflix-using-natural-language-processing-53fdbcf94417 "Medium") 

Average Word2Vec model:

The results of average Word2Vec vectorization based model are not very relevant. The reason behind this is our idea to combine first and last names like ‘samueljackson’ to form a unique word in our text string to get rid of similarity perception our distance based similarity model might have between people having same first names. This technique works wonderfully well for other vectorization models. Unfortunately, these words do not exist in our word2vecmodel provided by Google. To make up for this discrepancy we assign zeros to all 300 dimensions of vector representing the word ‘samueljackson’ . Many such unique words in our corpus end up becoming zero vectors and do not contribute to the average word to vector conversion of our sentences. This leads to placing of the vector representing a movie in a region of vectors with not very similar movies due to zero vector representation of certain words in the strings.

Tfidf & Bag of words:

Seeing our results for bag of words and Tfidf vectorization models, we cannot determine which vectorization model is giving us better results. To find out which model is better we would have to first live test our recommendation models. We would divide our customers into random test groups of equal sizes and live test a model on each group. Second step would be to collect various response parameters or business parameters such as purchase conversion rate of recommendations, recommendation selection rate etc. Third step would be to perform multivariate A/B testing using these parameters after collecting significant amount of data to select which is the better performing model.

### Improvements :
1. Word2Vec vectorization does not work well in our case because of the null vectors assigned to unique words not present in the Google's word to vec dictionary such as combination of cast first and last name as a single word, director first and last name as a single word etc. In order to make Word2Vec vectorization give more relevant results we will need to make our own Word2Vec dictionary using the corpus of words present in the relevant features of the dataset we model.

2. Seeing our results we cannot determine which vectorization model is giving us better results amongst bag of words, Tfidf and idf vectorized models. To find out which model is better we would have to first live test our recommendation models. We would divide our customers into random test groups of equal sizes and live test a model on each group. Second step would be to collect various response parameters or business parameters such as purchase conversion rate of recommendations, recommendation selection rate etc. Third step would be to perform multivariate A/B testing using these parameters after collecting sufficiently large data to select the best performing model.

## Licensing, Authors, Acknowledgements<a name="licensing"></a>
Credit to Netflix for providing the data.
