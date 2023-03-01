**SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report #3 – Code Coverage, Adequacy Criteria and Test Case Correlation**

| Group \#:      |     |
| -------------- | --- |
| Student Names: |     |
| Jack Rovere               |  30085670   |
|                |     |
|                |     |

(Note that some labs require individual reports while others require one report
for each group. Please see each lab document for details.)

# 1 Introduction

Text…

For DataUtilities, original Statement coverage was 48.7%, branch coverage was 29.7%, and method coverage was 60%. 

# 2 Manual data-flow coverage calculations for X and Y methods

Text…

# 3 A detailed description of the testing strategy for the new unit test

Text…

# 4 A high level description of five selected test cases you have designed using coverage information, and how they have increased code coverage

Text…

# 5 A detailed report of the coverage achieved of each class and method (a screen shot from the code cover results in green and red color would suffice)

DataUtilities:

<img width="328" alt="image" src="https://user-images.githubusercontent.com/98235387/222014564-00cfc318-bd51-48f2-8d4a-69ad30d7fd8e.png">
<img width="392" alt="image" src="https://user-images.githubusercontent.com/98235387/222014594-41f6ad06-142f-429c-b04f-524b8d0c03c2.png">
<img width="393" alt="image" src="https://user-images.githubusercontent.com/98235387/222014616-87e3374c-ecbc-45b6-ab51-4347b63926cf.png">
<img width="384" alt="image" src="https://user-images.githubusercontent.com/98235387/222014667-9032eb40-6651-4d7d-8246-ab4b592ed4fb.png">
<img width="363" alt="image" src="https://user-images.githubusercontent.com/98235387/222014685-4be47b3e-9164-432b-9d55-81df917fb2d0.png">
<img width="352" alt="image" src="https://user-images.githubusercontent.com/98235387/222014702-12a7fc97-a083-4633-96be-e762071fee42.png">
<img width="324" alt="image" src="https://user-images.githubusercontent.com/98235387/222014738-eb6c5f06-5d15-4c5f-b58d-438a41da340a.png">
<img width="358" alt="image" src="https://user-images.githubusercontent.com/98235387/222014759-85e6bb9d-a7df-4642-88ef-b56417e4d034.png">
<img width="424" alt="image" src="https://user-images.githubusercontent.com/98235387/222014782-fce55e92-8fc5-43d5-8ca8-20cde629bf49.png">

For DataUtilities, the new Statement coverage was 88.5%. This number could not be higher as in the DataUtilities class, several methods such as calculateColumnTotal had infinite loops, where if the code entered that space it would not be able to end. The Branch coverage was 71.9%, a large increase from the first implementation of the unit testing. Since EclEmma cannot analyze for condition coverage, we looked at the Method coverage instead, which is 100%, as all methods were accounted for.


# 6 Pros and Cons of coverage tools used and Metrics you report

Text…

# 7 A comparison on the advantages and disadvantages of requirements-based test generation and coverage-based test generation.

Text…

# 8 A discussion on how the team work/effort was divided and managed

Text…

# 9 Any difficulties encountered, challenges overcome, and lessons learned from performing the lab

Text…

# 10 Comments/feedback on the lab itself

Text…
