
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
The punctuation can be removed by tokenization. The regular expression \w+ keeps only words and discards anything else. Additional preprocessing can be performed using stopwords.  The reason why stop words are critical is that, if we remove the words that are very commonly used in a given language, we can focus on the important words instead. Stopwords can be filtered by maintaining the list of commonly used words that does not add any value to distinctly identify the document.
StopWords.txt file can be updated with uninterested/commonly used conjunctions and  prepositions for better text mining results.






**Test suite can be squeezed by combining functionally related test cases**
![image](https://user-images.githubusercontent.com/4659907/49638785-43a39100-fa2f-11e8-9a6e-e6fdaf49ed15.png)



**Terms of use:**
Orange is an open source project. If you include it within your programs, please comply with the [licence](https://orange.biolab.si/license/). It is attributed to  Orange, Data Mining Fruitful & Fun.For more details visit http://orange.biolab.si/



