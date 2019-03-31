
## **Squeeze Test Suite using Orange**

**What is it?**

Selection of distinct test case in a test suite by eliminating the duplicate test cases and merging of functionally related test cases are the two major challenges in testing of a product. As a solution to these problems, I propose a data mining based model that anyone can use. This solution provides visual representation of two or more test case pairs in a test suite that are identical or functionally related. This can be used as an input in order to eliminate the duplicate test cases and also for functionally merging the test cases; thus making a leaner test suite.

![untitled diagram](https://user-images.githubusercontent.com/4659907/53282506-7c195800-375e-11e9-8c13-3241711c6bde.jpg)

**Coming to the point..**
The model developed for this is developed using Orange. Orange is a comprehensive, component-based software suite for machine learning and data mining.

Pre-requisite:
A capability must be established to save the test cases in a test suite or test plan folder of interest as individual text files in a folder. This serves as input to the model. If any test case contains any attachments that needs to be ignored. If the test cases are managed in HP ALM, this can be established using REST API of ALM.

**1. Setting up Orange:**

Download latest version of Orange from [here]( https://orange.biolab.si/download/)
![image](https://user-images.githubusercontent.com/4659907/48974700-3e386500-f085-11e8-8d69-6dbe96baa3a1.png)

**2. Install Text Add-on in Orange:**
In Orange canvas Navigate to Options -> Add-ons. Search "Text" Add-on and install.
![image](https://user-images.githubusercontent.com/4659907/48977956-89289b80-f0ca-11e8-80bc-d300ee3fdbb8.png)


**3. Open Workflow**
Download or clone project squeeze-test-suite. Open workflow file "SqueezeTestSuite.ows" from File menu of orange canvas.

![image](https://user-images.githubusercontent.com/4659907/48978565-05bf7800-f0d3-11e8-9f25-801fd28ba6b7.png)


**4. Import documents**
Click on "Import Documents" widget and import test case folder of choice. For the purpose of demonstrating I have imported the sample test cases for google search written in Gherkin syntax from the folder "GherkinTests" provided in this repo.

![image](https://user-images.githubusercontent.com/4659907/49338041-0dd36680-f643-11e8-9cec-7c4383d6ae5f.png)

**5. View the documents**
Once the documents are imported, they can be viewed using Corpus viewer widget.

![image](https://user-images.githubusercontent.com/4659907/49342553-da183100-f682-11e8-94a5-80a93124e3ee.png)

**6 Text Preprocessing**
Preprocessing a text is a vital step in text mining. Let's inspect the  text without any preprocessing from the corpus using word cloud widget.


![image](https://user-images.githubusercontent.com/4659907/49342606-ae497b00-f683-11e8-959a-82a971a29617.png)

It's indeed a clutter!.. Without any preprocessing, the most frequent words are punctuations, conjunctions and prepositions!

![image](https://user-images.githubusercontent.com/4659907/49342754-15b3fa80-f685-11e8-80bf-3ced2fb3eebb.png)

With preprocessing we can remove these frequently used and uninteresting words to get to the words of our interest.
**a. Tokenization:** Tokenization is the method of breaking the text into smaller components (words). punctuation can be removed by tokenization. The regular expression \w+ keeps only words and discards anything else.

**b.Normalization:** It applies stemming and lemmatization to words. Stemming is the process of producing morphological variants of a root/base word. Stemming programs are commonly referred to as stemming algorithms or stemmers. A stemming algorithm reduces the words “chocolates”, “chocolatey”, “choco” to the root word, “chocolate” and “retrieval”, “retrieved”, “retrieves” reduce to the stem “retrieve”.

**Eg:** I’ve always loved cats. → I have alway love cat. For languages other than English use Snowball Stemmer. 

Some more example of stemming for root word "like" include:
"likes", "liked", "likely","liking"

**c.Filtering:** Additional preprocessing can be performed using stopwords.  The reason why stop words are critical is that, if we remove the words that are very commonly used in a given language, we can focus on the important words instead. Stopwords can be filtered by maintaining the list of commonly used words that does not add any value to distinctly identify the document.
StopWords.txt file can be updated with uninterested/commonly used conjunctions and  prepositions for better text mining results.


Note: Preprocess Text applies preprocessing steps in the order they are listed. This means it will first transform the text, then apply tokenization and so on..

**7. Bag of words** :
Bag of words model creates a corpus with word counts for each data instance (document). The count can be either absolute, binary (contains or does not contain) or sublinear (logarithm of the term frequency). 

Vector space model: Given the bag of words that we extract from the document, we create a feature vector for the document, where each feature is a word (term) and the feature's value is a term weight. The term weight can be calculated using **TF-IDF** (term frequency – inverse document frequency)
![image](https://user-images.githubusercontent.com/4659907/55291768-61db3580-5400-11e9-8c39-2ec5399d2972.png)

The entire document is thus a feature vector, and each feature vector corresponds to a point in a vector space. The model for this vector space is such that there is an axis for every term in the vocabulary, and so the vector space is V-dimensional, where V is the size of the vocabulary. The vector should then conceptually also be V-dimensional with a feature for every vocabulary term. 


Term frequency (tf) is basically the output of the Bag of words model. For a specific document, it determines how important a word is by looking at how frequently it appears in the document. Term frequency measures the local importance of the word. If a word appears a lot of times, then the word must be important. For example, if our document is  “I am a cat lover. I have a cat named Steve. I feed a cat outside my room regularly,” we see that the words with the highest frequency are I, a, and cat. This agrees with our intuition that high term frequency = higher importance since the document is all about my fascination with cats.

The second component of tf-idf is inverse document frequency (idf). For a word to be considered a signature word of a document, it shouldn’t appear that often in the other documents. Thus, a signature word’s document frequency must be low, meaning its inverse document frequency must be high. The tf-idf is usually calculated as:
![image](https://user-images.githubusercontent.com/4659907/55291604-d52f7800-53fd-11e9-9766-dff61e6f72f8.png)

![image](https://user-images.githubusercontent.com/4659907/55291586-98fc1780-53fd-11e9-8919-f4b1eeb99b7e.png)

**8. Distances**:
This widget computes the distances between rows/columns in a dataset.

Inputs
Data: input dataset

Outputs
Distances: distance matrix

In this case the Distance Metric is choosen as Euclidean (“straight line”, shortest distance between two points).

![image](https://user-images.githubusercontent.com/4659907/55292112-4114df00-5404-11e9-850d-b68d7ac662a9.png)

If the distance is 0, it means that both objects are identical. The resulting distance matrix can be fed further to MDS(Multi Dimensional scaling) for mapping the data instances using the distance matrix.

**9.Dimensionality reduction using MDS(Multi Dimensional scaling)**:
Multidimensional scaling is a technique which finds a low-dimensional (in our case a two-dimensional) projection of points, where it tries to fit distances between points as well as possible.




**Terms of use:**
Orange is an open source project. If you include it within your programs, please comply with the [licence](https://orange.biolab.si/license/). It is attributed to  Orange, Data Mining Fruitful & Fun.For more details visit http://orange.biolab.si/



