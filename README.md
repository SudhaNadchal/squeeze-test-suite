
**What is it?**
Selection of distinct test case in a test suite by eliminating the duplicate test cases and merging of functionally related test cases are the two major challenges in product testing. As a solution to these problems, I propose a data mining based model that anyone can use. This solution provides visual representation of two or more test case pairs in a test suite that are identical or functionally related. This can be used as an input in order to eliminate the duplicate test cases and also for functionally merging the test cases; thus making a leaner test suite.

**Coming to the point..**
The model developed for this is developed using Orange. Orange is a comprehensive, component-based software suite for machine learning and data mining.

Pre-requisite:
A capability must be established to save the test cases in a test suite or test folder of interest as individual text files in a folder. This serves as input to the model. If any test case contains any attachments that needs to be ignored. If the test cases are managed in HP ALM, this can be established using REST API of ALM.

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
Click on "Import 










**Terms of use:**
Orange is an open source project. If you include it within your programs, please comply with the [licence](https://orange.biolab.si/license/). It is attributed to  Orange, Data Mining Fruitful & Fun.For more details visit http://orange.biolab.si/



