**SENG 438 - Software Testing, Reliability, and Quality**

**Lab. Report #3 – Code Coverage, Adequacy Criteria and Test Case Correlation**

| Group \#:      |   7  |
| -------------- | --- |
|Brenek Spademan               |30060822    |
|Ben Leggett                |30114359     |
|Arion Hamel                |30112662     |
|Jack Rovere                |30085670     |

(Note that some labs require individual reports while others require one report
for each group. Please see each lab document for details.)

# 1 Introduction

In this lab, we looked back at our unit tests created in Assignment 2. With our new code coverage tool EclEmma, we dissected our tests and saw how much code they covered in multiple metrics. We then created new unit tests to increase the coverage of our code, and reported these results.

For DataUtilities, original Statement coverage was 48.7%, branch coverage was 29.7%, and method coverage was 60% according to EclEmma. 

For RangeTest, original Statement coverage was 14.3%, branch coverage was 12.2%, and method coverage was 26.1% according to EclEmma.

# 2 Manual data-flow coverage calculations for X and Y methods

## __DataUtilities:__

  __Data Flow Graph:__

  <img width="513" alt="image" src="https://user-images.githubusercontent.com/98235387/222039083-9af332e6-6e0f-49c9-b92b-dd505f8ee3fb.png">
  
  __def-use sets per statement:__
  
  DEF(1) = {data, column}, USE(1) = {data} <br>
  DEF(2) = {total}, USE(2) = {} <br>
  DEF(3) = {rowCount}, USE(3) = {data} <br>
  DEF(4) = {r}, USE(4) = {r, rowCount} <br>
  DEF(5) = {n}, USE(5) = {data, r, column} <br>
  DEF(6) = {}, USE(6) = {n} <br>
  DEF(7) = {}, USE(7) = {total, n} <br>
  DEF(8) = {}, USE(8) = {r} <br>
  DEF(9) = {r2}, USE(9) = {r2, rowCount} <br>
  DEF(10) = {n}, USE(10) = {data, r2, column} <br>
  DEF(11) = {}, USE(11) = {n} <br>
  DEF(12) = {}, USE(12) = {total, n} <br>
  DEF(13) = {}, USE(13) = {r2} <br>
  DEF(14) = {}, USE(14) = {total} <br>
  
  __DU pairs per variable:__
  
  <img width="260" alt="image" src="https://user-images.githubusercontent.com/98235387/222044488-fbed8adf-578b-4922-93fa-97fd817ff4c5.png">

  __pairs covered per test case:__
  
  <img width="609" alt="image" src="https://user-images.githubusercontent.com/98235387/222047619-208647c3-a69f-4a96-9a92-9c20ef22e28f.png">
  
  __DU pair coverage:__
  
  Total C-use: 12 <br>
  Total P-use: 7 <br>
  C-use by Test: 7 (infeasible 5) <br>
  P-use by Test: 5 (infeasable 1) <br>
  DU pair coverage = (7 + 5) / [(12 + 7) - (5 + 1)] <br>
  DU pair coverage = 92.3%
  
  
# 3 A detailed description of the testing strategy for the new unit test

<h2>DataUtilities Testing | Jack & Arion </h2>

Before beginning testing we go through a setUp() process, in which we create a new Mockery object to mock Values2D and KeyedValues objects. These Mockery objects were used in conjunction with EclEmma to measure the statement, branch and method coverage of the DataUtilities class. 

<h3>1. equal(double[][] a, double[][] b)</h3>

equal() receives two 2D arrays and returns a boolean value to express if they are equal.

* First test: ‘equalWhenOnlyANull()’ is a simple assertFalse statement, in which we pass a null value with a new 2D array. The function should return false. 

* Second test: 'equalWhenOnlyBNull()' is another assertFalse statement, in which we pass a new 2D array with a null value. The function should return false. 

* Third test: 'equalWhenBothNull()' is an assertTrue statement, in which we pass two null values as arguments. The function should return true. 

* Fourth test: 'equalWhenBothEqual()' is an assertTrue statement, in which we pass two identical 2D arrays. The function should return true.

* Fifth test: 'equalWhenLengthNotEqual()' is an assertFalse statement, in which we pass two 2D arrays; however one is a different sice. The function should return false. 

In testing equal() we did not make use of mocking and through the use of EclEmma we reached 100% in statement, branch, and method coverage areas. 

<h3>2. clone(double[][] source)</h3>

clone() receives a 2D array of type double, and returns a seperate identical 2D array of type double. 
   
* First test: 'cloneClonesProperlyOnPositiveValue()' creates a 'double[][] original' with values {{1.0}}. This 2D array is passed into clone, which returns a clone into 'double[][] cloned'. 'cloneClonesProperlyOnPositiveValue()' runs an assertEquals on 'original' and 'cloned' in order to ensure they are identical. The assertEquals should pass.

* Second test: 'cloneClonesProperlyOnNegativeValue()' creates a 'double[][] original' with values {{-1.0}}. This 2D array is passed into clone, which returns a clone into 'double[][] cloned'. 'cloneClonesProperlyOnPositiveValue()' runs an assertEquals on 'original' and 'cloned' in order to ensure they are identical. The assertEquals should pass.

In testing clone() we did not make use of mocking. Testing both positive and negative values is used as a sort of boundary and equivalent testing. We reached 100% for statement and method coverage, and 75% for branch coverage. 

<h3>3. calculateColumnTotal(Values2D data, int column)</h3>
   
Each function utilizes as Values2D mock when summing the values in the column provided. calculateColumnTotal sums the values in a Values2D object, through the column provided. 

* First test: 'calculateColumnTotalForFourPositiveValues()' mocks a Values2D object as follows: {3.0, 2.5, 7.0, 10.5} in (0,0), (1,0), (2,0), and (3,0) respectively. The test method expects a sum of 23.0 to be returned.

* Second test: 'calculateColumnTotalForFourNegativeValues()' is similar to the test above, differing by only inputting negative values in the Values2D object. The mock Values2D object is as follows: {-1.0, -2.5, -7.0, -14.5} in (0,0), (1,0), (2,0), and (3,0) respectively. The test method expects a sum of -25.0 to be returned.

* Third test: 'exceptionThrownOnInvalidDataColumn()' provides an invalid Values2D argument. As per the documentation of calculateColumnTotal(), an 'InvalidParameterException' should be thrown. exceptionThrownOnInvalidDataColumn ensures that the proper exception is thrown from calculateColumnTotal().

We test both negative and positive numbers as a form of equivalence partitioning and boundary value analysis. 'exceptionThrownOnInvalidDataColumn()' involves use case testing, in a scenario where a user inputs incorrect data to the function. We reached 91.7%, 75.0%, and 100% for our statement, branch, and method coverage respectively.

<h3>4. calculateColumnTotal(Values2D data, int column, int[] validRows)</h3>

Each function utilizes as Values2D mock when summing the values in the column provided. calculateColumnTotal sums the column and rows provided in the Values2D object given. 

* First test: 'calculateColumnTotalForFourPositiveValuesValid()' mocks a Values2D object as follows: {3.0, 2.5, 7.0, 10.5} in (0,0), (1,0), (2,0), and (3,0) respectively. We also use mocking to ensure that getRowCount() returns 4; matching our provided validRows argument. The test method expects a sum of 23.0 to be returned.

* Second test: 'calculateColumnTotalForFourNegativeValuesValid()' is similar to the test above, differing by only inputting negative values in the Values2D object. The mock Values2D object is as follows: {-1.0, -2.5, -7.0, -14.5} in (0,0), (1,0), (2,0), and (3,0) respectively. We also use mocking to ensure that getRowCount() returns 4; matching our provided validRows argument. The test method expects a sum of -25.0 to be returned.

* Third test: 'calculateColumnTotalRowCountInvalid()' mocks a Values2D object as follows: {3.0, 2.5, 7.0, 10.5} in (0,0), (1,0), (2,0), and (3,0) respectively. However, we ensure getRowCount() returns 0 through mocking; contradicting our provided validRows argument. The test should fail. 

We test both negative and positive numbers as a form of equivalence partitioning and boundary value analysis. We reached 75.0%, 50.0%, and 100% for our statement, branch, and method coverage respectively.

<h3>5. calculateRowTotal(Values2D data, int row)</h3>

Each function utilizes as Values2D mock when summing the values in the row provided. calculateColumnTotal sums the values in a Values2D object, through the row provided. 
   
* First test: 'calculateRowTotalForFourPositiveValues()' mocks a Values2D object as follows {3.5, 2.0, 7.5, 15.0} in (0, 0), (0, 1), (0, 2), and (0, 3) respectively. The test method expects a sum of 28.0 to be returned.

* Second test: 'calculateRowTotalForFourNegativeValues()' mocks a Values2D object as follows {-2.5, -5.5, -7.5, -15.0} in (0, 0), (0, 1), (0, 2), and (0, 3) respectively. The test method expects a sum of -30.5 to be returned.

* Third test: 'exceptionThrownOnInvalidDataRow()' provides an invalid Values2D argument. As per the documentation of calculateRowTotal(), an 'InvalidParameterException' should be thrown. exceptionThrownOnInvalidDataColumn ensures that the proper exception is thrown from calculateRowTotal().

We test both negative and positive numbers as a form of equivalence partitioning and boundary value analysis. 'exceptionThrownOnInvalidDataRow()' involves use case testing, in a scenario where a user inputs incorrect data to the function. We reached 91.7%, 75.0%, and 100% for our statement, branch, and method coverage respectively.

<h3>6. calculateRowTotal(Values2D data, int row, int[] validCols)</h3>

Each function utilizes as Values2D mock when summing the values in the row provided. calculateColumnTotal uses the columns provided to sum the row given in our mocked Values2D object. 

* First test: 'calculateRowTotalForFourPositiveValuesValid()' mocks a Values2D object as follows {3.0, 2.5, 7.0, 10.5} in (0, 0), (0, 1), (0, 2), and (0, 3) respectively. We then provide {0, 1, 2, 3} as valid columns to be summed, matching our mocked getColumnCount() value. The test method expects a sum of 23.0 to be returned. 

* Second test: 'calculateRowTotalForFourNegativeValuesValid()' mocks a Values2D object as follows {-1.0, -2.5, -7.0, -14.5} in (0, 0), (0, 1), (0, 2), and (0, 3) respectively. We then provide {0, 1, 2, 3} as valid columns to be summed, matching our mocked getColumnCount() value. The test method expects a sum of -25.0 to be returned.

* Third test: 'calculateRowTotalColumnCountInvalid()' mocks a Values2D object as follows: {3.0, 2.5, 7.0, 10.5} in (0,0), (1,0), (2,0), and (3,0) respectively. However, we ensure getColumnCount() returns 0 through mocking; contradicting our provided validColumns argument. The test should fail. 

We test both negative and positive numbers as a form of equivalence partitioning and boundary value analysis. We reached 75.0%, 50.0%, and 100% for our statement, branch, and method coverage respectively.

<h3>7. createNumberArray(double[] data)</h3>

There are no mocking objects used in the following test cases.

createNumberArray takes in an array of doubles, and creates an array of Number objects.

* First test: 'createEmptyNumberArray()' creates a 'double[] data' with no values inside. It is then passed towards DataUtilities.createNumberArray() as an argument. The test case expects 'createNumberArray()' to return an empty array of Number objects.

* Second test: 'createNumberArrayPositiveValues()' passes a 'double[] data' with values = {1.0, 2.0, 3.0, 4.0, 5.0} into DataUtilites.createNumberArray(). The test case expects 'createNumberArray()' to return an array of Number objects = {1.0, 2.0, 3.0, 4.0, 5.0}. 

* Third test: 'createNumberArrayNegativeValues()' passes a 'double[] data' with values = {-1.0, -2.0, -3.0, -4.0, -5.0}. It is then passed towards Data.Utilities.createNumberArray() as an argument. The test case expects 'createNumberArray()' to return an array of Number objects = {-1.0, -2.0, -3.0, -4.0, -5.0}.
    
We test both negative and positive numbers as a form of equivalence partitioning and boundary value analysis. createEmptyNumberArray() acts as a boundary value and use case test, evaluating how the function behaves with an unexpected input. We reached 100% for our statement, branch, and method coverage.

<h3>8. createNumberArray2D(double[][] data)</h3>

There are no mocking objects used in the following test cases.

createNumberArray2D takes in a double (2D) array of doubles, and creates a 2D array of Number objects.

* First test: 'createEmpty2DNumberArray()' creates a 'double[][] data' with no values inside. It is then passed towards DataUtilities.createNumberArray2D() as an argument. The test case expects 'createNumberArray2D()' to return an empty 2D array of Number objects.

* Second test: 'create2DNumberArrayPositiveValues()' passes a 'double[][] data' with values = {{1.0, 2.0, 3.0, 4.0, 5.0}, {6.0, 7.0, 8.0}, {1.0}} into DataUtilites.createNumberArray2D(). The test case expects 'createNumberArray2D()' to return a 2D array of Number objects = {{1.0, 2.0, 3.0, 4.0, 5.0}, {6.0, 7.0, 8.0}, {1.0}}. 

* Third test: 'create2DNumberArrayNegativeValues()' passes a 'double[] data' with values = {{-1.0, -2.0, -3.0, -4.0, -5.0}, {-6.0, -7.0, -8.0}, {-1.0}}. It is then passed towards Data.Utilities.createNumberArray2D() as an argument. The test case expects 'createNumberArray2D()' to return a 2D array of Number objects = {{-1.0, -2.0, -3.0, -4.0, -5.0}, {-6.0, -7.0, -8.0}, {-1.0}}.
    
We test both negative and positive numbers as a form of equivalence partitioning and boundary value analysis. createEmptyNumberArray2D() acts as a boundary value and use case test, evaluating how the function behaves with an unexpected input. 

Neither createNumberArray or createNumberArray2D's tests utilize mocking, thus a discussion of mocking's benefits and drawbacks is not applicable.We reached 100% for our statement, branch, and method coverage.

<h3>9. getcumulativePercentages(KeyedValues Data)</h3>

Each test utilizes the KeyedValues mocking object created above. 

DataUtilities.getCumulativePercentages() receives a KeyedValues object - containing key/value pairs - and returns a KeyedValues object in which each key/value pair represents the cumulative percentage thus far of each key/value pair provided. 

* First test: 'exceptionThrownOnInvalidPercentageData()' passes an invalid argument to 'DataUtilites.getCumulativePercentages()'. Given the documentation of 'getCumulativePercentages()', the test case expects an 'InvalidParameterException' to be thrown. 

* Second test: 'cumulatePercentageForZeroValueKeyPairs()' creates a 'String[] names' with values = {"KeyOne", "KeyTwo", "KeyThree"} and a 'double[] values' with values = {0, 0, 0}. This simulates the data in a KeyedValues object as follows: (KeyOne, 0), (KeyTwo, 0), (KeyThree, 0). The test case expects 'getCumulativePercentages()' to return a NaN Divide by zero, as there should be a divide by zero error in calculating the cumulative percentage. 

* Third test: 'cumulatePercentageForPositiveValueKeyPairs()' creates a 'String[] names' with values = {"KeyOne", "KeyTwo", "KeyThree"} and a 'double[] values' with values = {5.0, 9.0, 2.0}. This simulates the data in a KeyedValues object as follows: (KeyOne, 5.0), (KeyTwo, 9.0), (KeyThree, 2.0). The test case expects 'getCumulativePercentages()' to return 0.3125 when queried for the value of the resultant KeyOne.

* Fourth test: 'cumulatePercentageForNegativeValueKeyPairs()' creates a 'String[] names' with values = {"KeyOne", "KeyTwo", "KeyThree"} and a 'double[] values' with values = {-5.0, -9.0, -2.0}. This simulates the data in a KeyedValues object as follows: (KeyOne, -.50), (KeyTwo, -9.0), (KeyThree, -2.0). The test case expects 'getCumulativePercentages()' to return 0.3125 when queried for the value of the resultant KeyOne.
    
We test both negative and positive numbers as a form of equivalence partitioning and boundary value analysis. exceptionThrownOnInvalidPercentageData() acts as a boundary value and use case test, evaluating how the function behaves with an unexpected input, and ensuring an 'InvalidParameterException' is properly thrown. Similarly 'cumulatePercentageForZeroValueKeyPairs()' is a boundary value and use case test, as it provides an unusual input that should provide an error if handled properly. 

Mocking in 'getCumulativepercentages()' was useful in isolated the test component and functionality being testing. We effectively eliminated the KeyedValues class dependency, and were able to manufacture our expected output, and test accordingly. However the tests became significantly more complex and may not accurately reflect the behaviour of the code in a real-world scenario. Using KeyedValues objects may produce differing results. 

We reached 88.5%, 71.9%, and 100% for our statement, branch, and method coverage respectively. 

# 4 A high level description of five selected test cases you have designed using coverage information, and how they have increased code coverage

Text…

# 5 A detailed report of the coverage achieved of each class and method (a screen shot from the code cover results in green and red color would suffice)

## __DataUtilities:__

<img width="328" alt="image" src="https://user-images.githubusercontent.com/98235387/222014564-00cfc318-bd51-48f2-8d4a-69ad30d7fd8e.png">
<img width="392" alt="image" src="https://user-images.githubusercontent.com/98235387/222014594-41f6ad06-142f-429c-b04f-524b8d0c03c2.png">
<img width="393" alt="image" src="https://user-images.githubusercontent.com/98235387/222014616-87e3374c-ecbc-45b6-ab51-4347b63926cf.png">
<img width="384" alt="image" src="https://user-images.githubusercontent.com/98235387/222014667-9032eb40-6651-4d7d-8246-ab4b592ed4fb.png">
<img width="363" alt="image" src="https://user-images.githubusercontent.com/98235387/222014685-4be47b3e-9164-432b-9d55-81df917fb2d0.png">
<img width="352" alt="image" src="https://user-images.githubusercontent.com/98235387/222014702-12a7fc97-a083-4633-96be-e762071fee42.png">
<img width="324" alt="image" src="https://user-images.githubusercontent.com/98235387/222014738-eb6c5f06-5d15-4c5f-b58d-438a41da340a.png">
<img width="358" alt="image" src="https://user-images.githubusercontent.com/98235387/222014759-85e6bb9d-a7df-4642-88ef-b56417e4d034.png">
<img width="424" alt="image" src="https://user-images.githubusercontent.com/98235387/222014782-fce55e92-8fc5-43d5-8ca8-20cde629bf49.png">

## __Statement:__
<img width="232" alt="image" src="https://user-images.githubusercontent.com/98235387/222046020-45cf7000-2a93-472f-8160-bf1df22e41a8.png">

## __Branch:__
<img width="230" alt="image" src="https://user-images.githubusercontent.com/98235387/222046133-880faf5b-4048-47f0-96d7-390f2b1c5901.png">

## __Method:__
<img width="303" alt="image" src="https://user-images.githubusercontent.com/98235387/222046189-7d8b802e-280d-42d7-b292-72f81871e95f.png">


For DataUtilities, the new Statement coverage was 88.5%. This number could not be higher as in the DataUtilities class, several methods such as calculateColumnTotal had infinite loops, where if the code entered that space it would not be able to end. The Branch coverage was 71.9%, a large increase from the first implementation of the unit testing. Since EclEmma cannot analyze for condition coverage, we looked at the Method coverage instead, which is 100%, as all methods were accounted for.


## __Range:__
<img width="1115" alt="Screen Shot 2023-03-02 at 10 17 06 AM" src="https://user-images.githubusercontent.com/101214266/222503127-1c6a4834-103d-4e68-9515-27fdf10e5470.png">
<img width="1083" alt="Screen Shot 2023-03-02 at 10 17 25 AM" src="https://user-images.githubusercontent.com/101214266/222503184-9f5b7829-1eed-494f-985c-cca5422b09c8.png">
<img width="1103" alt="Screen Shot 2023-03-02 at 10 17 42 AM" src="https://user-images.githubusercontent.com/101214266/222503248-85aaab6a-8017-432a-b742-9795ac4026b5.png">
<img width="1103" alt="Screen Shot 2023-03-02 at 10 18 06 AM" src="https://user-images.githubusercontent.com/101214266/222503341-57c92629-2d67-4b69-b8a1-b0fec839a623.png">



## __Statement:__


## __Branch:__


## __Method:__



For DataUtilities, the new Statement coverage was 88.5%. This number could not be higher as in the DataUtilities class, several methods such as calculateColumnTotal had infinite loops, where if the code entered that space it would not be able to end. The Branch coverage was 71.9%, a large increase from the first implementation of the unit testing. Since EclEmma cannot analyze for condition coverage, we looked at the Method coverage instead, which is 100%, as all methods were accounted for.


# 6 Pros and Cons of coverage tools used and Metrics you report

Utilizing EclEmma allowed us to view the coverages our test cases provided. Its robust ability to function with mockery objects permitted us to retain much of our original test cases, and expand upon features through white-box testing. The coverage data is useful in understanding test case effectiveness. It was easy to use, clear; and useful. However, EclEmma lacks coverage options, forcing us to analyze method coverage as opposed to condition coverage. 

# 7 A comparison on the advantages and disadvantages of requirements-based test generation and coverage-based test generation.

<h3>Requirements-Based</h3>

Requirements based testing utilizes specific requirements in order to design the tests. Developers can achieve a higher probability of detecting defects, ensure requirements are met, and can help reduce the number of tests needed. However obtaining the specific requirements is difficult and time consuming. It can also be challenging to maintain, as the test suite may fluctuate frequently.

<h3>Coverage-Based</h3>

Coverage based testing analyzes the coverages of each code path, allowing developers to measure the quality of the test suite and can help detect defects that might be missed. However, not all defects may be found, and it can be time-consuming to develop and maintain redundant test cases. Additionally, some coverage may not be feasibly tested.

# 8 A discussion on how the team work/effort was divided and managed

<h3> Brenek & Ben</h3>

<h3> Jack & Arion</h3>

Jack implemented the new test cases and managed the coverage details. He also worked on the dataflow diagrams above. Arion created the test plan and aided Jack where possible through peer programing.

# 9 Any difficulties encountered, challenges overcome, and lessons learned from performing the lab

<h3> Brenek & Ben</h3>

<h3> Jack & Arion</h3>

One large difficulty in DataUtilities was the inability to achieve higher than 88.5% Statement coverage, as there was an infinite loop in the code. This was discovered by looking at the error output from the mocking, which lead us to realize that the error was present and we could not increase our coverage in this way without breaking our code. We resolved this issue by focusing our coverage onto other parts of the code that were not as broken.

# 10 Comments/feedback on the lab itself

We all found this lab to be more interesting than the ones before. We also felt as though this lab was very good practice for the approaching midterm, as it gave us plenty of knowledge with not only unit testing and coverage, but also DU pairs and data flow charts.
