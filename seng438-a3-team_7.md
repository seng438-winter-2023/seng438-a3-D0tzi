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
  
  
  ## __Range:__

  __Data Flow Graph:__  
  
  ![image](https://user-images.githubusercontent.com/101438680/222543668-c24f0fe8-a30a-4934-a523-1515a5a7e74a.png)
  
 __def-use sets per statement:__

DEF(0) = {lower, upper}, USE(0) = {}  
DEF(1) = {b0, b1}, USE(1) = {b0, lower}  
DEF(2) = {}, USE(2) = {b1, lower}  
DEF(3) = {}, USE(3) = {b0, b1, upper}  

 __DU pairs per variable:__

![image](https://user-images.githubusercontent.com/101438680/222543760-44e35df6-bb33-4b3b-8690-23156cbad35c.png)

 __pairs covered per test case:__

![image](https://user-images.githubusercontent.com/101438680/222544008-42fabd71-8b16-4daa-8df1-46201b46a1c1.png)


 __DU pair coverage:__

Total C-use: 0  
Total P-use: 3  
C-use by Test: 0 (infeasible 0)  
P-use by Test: 2 (infeasable 1)  
DU pair coverage = (0 + 2) / [(0 + 3) - (0 + 1)]   
DU pair coverage = 100.00%  

  
  
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

Each function utilizes as Values2D mock when summing the values in the row provided. calculateRowTotal uses the rows provided to sum the row given in our mocked Values2D object. 

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

<h2>Range Testing | Brenek & Ben </h2>

No mocking objects were created for any of the following methods of the Range function and their repsective tests. A Range object called 'exampleRange' was created witha lower and upper bound of -1 and 1 respectively to be used in tests where neccassary. 
<h3>1. getLowerBound()</h3>

getLowerBound returns the lower bound for the created Range object. 

* First test: 'lowerBoundShouldBeNegativeOne()' uses the Range object 'exampleRange' and calls the 'getLowerBound()' function to return the lower bound for the object. The expected return value is a value of -1 for a range containing both poitive and negative values.  
* Second test: 'lowerBoundShouldBeZero()' creates a new Range object with an lower and upper bound of 0 and 100 respectively. The 'getLowerBound()' method is then called, and the expected return value is 0.  
* Third test: 'lowerBoundShouldBe100()' creates a new Range object with an lower and upper bound of 100 and 200 respectively. The 'getLowerBound()' method is then called, and the expected return value is 100 for a range containing only positive values.  
* Fourth test: 'lowerBoundShouldBeNegative100()' creates a new Range object with an lower and upper bound of -100 and -50 respectively. The 'getLowerBound()' method is then called, and the expected return value is -50 for a range containing only negative values.  

We test both negative and positive numbers as a form of equivalence partitioning and boundary value analysis. We test the output of ranges spanning over both positive and negative values, all positive and all negative values.  

<h3>2. getUpperBound()</h3>

getUpperBound returns the upper bound for the created Range object. 

* First test: 'upperBoundShouldBeOne()' uses the Range object 'exampleRange' and calls the 'getUpperBound()' function to return the upper bound for the object. The expected return value is a value of 1 for a range containing both poitive and negative values.  
* Second test: 'upperBoundShouldBeOneHundred()' creates a new Range object with an lower and upper bound of 0 and 100 respectively. The 'getUpperBound()' method is then called, and the expected return value is 100.  
* Third test: 'upperBoundShouldZero()' creates a new Range object with an lower and upper bound of -50 and 0 respectively. The 'getUpperBound()' method is then called, and the expected return value is 0.  
* Fourth test: 'upperBoundShouldBeNegativeOneHundred()' creates a new Range object with an lower and upper bound of -500 and -100 respectively. The 'getUpperBound()' method is then called, and the expected return value is -100.  

We test both negative and positive numbers as a form of equivalence partitioning and boundary value analysis. We test the output of ranges spanning over both positive and negative values, all positive and all negative values. We have created tests with ranges where either the upper or lower bound is 0 in order to ensure that any unexpected behaviour is able to be observed in these situations.  

<h3>3. getLength()</h3>

getLength returns the value of the numeric range between the upper and lower bounds of the Range object.  

* First test: 'lengthShouldBeTwo()' uses the Range object 'exampleRange' and calls the 'getLength()' function to return the length of the specified range for the object. The expected return value is 2, and this test covers the scenerio where a range has both a positive and a negative bound.  
* Second test: 'lengthShouldBeFifty()' creates a new Range object with an lower and upper bound of -100 and -50 respectively. The expected return value is 50, and this test covers the scenerio where a range has both bounds as negative values.  
* Third test: 'lengthShouldBeOneHundred()' creates a new Range object with an lower and upper bound of -100 and 0 respectively. The expected return value is 100, and this test covers the scenerio where a range has a negative bound and a bound equal to 0.  
* Fourth test: 'lengthShouldBeTen()' creates a new Range object with an lower and upper of 0 and 10 respectively. The expected return value is 10, and this test covers the scenerio where a range has both a bound that is zero and a positive value.  
* Fifth test: 'lengthShouldBeTwenty()' creates a new Range object with an lower and upper bound of 20 and 40 respectively. The expected return value is 20, and this test covers the scenerio where a range has both bounds as positive values.  

We test both negative and positive numbers as a form of equivalence partitioning and boundary value analysis. We test the output of ranges spanning over both positive and negative values, all positive bounds or all negative values as bounds. We have created tests with ranges where either the upper or lower bound is 0 in order to ensure that any unexpected behaviour is able to be observed in these situations.  

<h3>4. getCentralValue()</h3>

getCentralValue returns the median value at thte middle of the upper and lower bounds of the Range object.  

* First test: 'centralValueShouldBeZero()' uses the Range object 'example Range' created with an upper bound of 1 and lower bound of -1. This test expects that a value of 0 is returned after calling exampleRange.getCentralValue().  
* Second test: 'centralValueShouldBeNegative150()' creates a new Range object with a lower and upper bound of (-200, -100) respectively. This test expects that a value of -150 is returned after calling exampleRange.getCentralValue().  
* Third test: 'centralValueShouldBe150()' creates a new Range object with a upper and lower bound of (200, 100) respectively. This test expects that a value of 150 is returned after calling exampleRange.getCentralValue().  

We test both negative and positive numbers as a form of equivalence partitioning and boundary value analysis. We test the output of a range spanning over both positive and negative values in the 'centralValueShouldBeZero()' test.  

<h3>5. contains(double value)</h3>

contains recieves a double value, returns true if the specified value is within the range, and false otherwise.  

* First test: 'rangeContains100()' creates a new Range object with a lower and upper bound of 50 and 150 respectively. The double value used when calling the 'contains()' function is 100, and the expected return value is true as the value of 100 is within the range.  
* Second test: 'rangeDoesNotContain49()' creates a new Range object with a lower and upper bound of 50 and 150 respectively. The double value used when calling the 'contains()' function is 49, and the expected return value is false as the value of 49 is not within the range. This observes the scenerio where the paramter passed to the contains() function is lower than the lower bound.  
* Third test: 'rangeDoesNotContain151()' creates a new Range object with a lower and upper bound of 50 and 150 respectively. The double value used when calling the 'contains()' function is 151, and the expected return value is false as the value of 151 is not within the range. This observes the scenerio where the paramter passed to the contains() function exceeds the upper bound.  
* Fourth test: 'rangeContainsZero()' uses the Range object 'exampleRange' and passes a value of 0 to the 'contains()' function. The expected output is true as 0 is within the range of the object. This covers a scenerio where the value is within the range, and the range bounds are both a negative and a positive value.  
* Fifth test: 'rangeDoesNotContainTwo()' uses the Range object 'exampleRange' and passes a value of 2 to the 'contains()' function. The expected output is false as 2 exceeds the upper limit of this Range object. This covers a scenerio where the value exceeds the range, and the range bounds are both a negative and a positive value.  
* Sixth test: 'rangeDoesNotContainNegativeTwo()' uses the Range object 'exampleRange' and passes a value of -2 to the 'contains()' function. The expected output is false as -2 less than the lower bound of the Range object. This covers a scenerio where the value is less than the lower bound, and the range bounds are both a negative and a positive value.  
* Seventh test: 'rangeContainsNegative100()' creates a new Range object with a lower and upper bound of -150 and -50 respectively. The double value used when calling the 'contains()' function is -100, and the expected return value is true as the value of -100 is within the range. Both the upper and lower bound values are negative.  
* Eighth test: 'rangeDoesNotContainNegative151()' creates a new Range object with a lower and upper bound of -150 and -50 respectively. The double value used when calling the 'contains()' function is -151, and the expected return value is false as the value of -151 is less than the lower bound.   
* Ninth Test: 'rangeDoesNotContainNegative49()' creates a new Range object with a lower and upper bound of -150 and -50 respectively. The double value used when calling the 'contains()' function is -49, and the expected return value is false as the value of -49 exceeds the range. Both the upper and lower bound values are negative.  

We test both negative and positive numbers as a form of equivalence partitioning and boundary value analysis. The case of a value being passed to the 'contains()' that is either too large for, too small for or within the range is tested in each possible scenerio regarding the upper and lower bounds and wether or not they are positive, negative or equal to zero.  

<h3>6. constrain(double value)</h3>

‘constrain’ receives a double value as its argument and returns the value in the range closest to the specified value.

* First test: ‘rangeConstrain3()’ creates a new Range object with an upper and lower bound of -1 and 1, as well as allocating a double value of 1. The ‘constrain’ method is then applied using an argument of ‘3.0’, and the expected result is true as the value provided from the method will be 1, the closest value from the established range of the new object.
* Second test: ‘rangeConstrainOne()’ creates a new Range object with an upper and lower bound of 2 and 3, as well as allocating a double value of 2. The ‘constrain’ method is then applied using an argument of ‘1.0’, and the expected result is true as the value provided from the method will be 2, the closest value from the established range of the new object. This considers a citation where the constrained value is within the range.


<h3>6. combine(Range range1, Range range2)</h3>

‘combine’ receives two different Range objects and creates a new range by combining the two existing ones. 

* First test: ‘range1NULLCombine()’ combines exampleRange with a null value. The expected return value is true as exampleRange has not been altered. 
* Second test: ‘‘range2NULLCombine()’ combines a null value with exampleRange. The expected return value is true as no alteration has been made to exampleRange. 
* Third test: ‘rangeCombine() ’ creates two new Range objects, first with a lower and upper bound of 0 and 2, and second with a lower and upper bound of -1 and 2. 

<h3>7. combineIgnoringNaN(Range range1, Range range2)</h3>

‘combineIgnoringNaN’ receives two Range objects and returns a new range spanning the ranges of both objects.

* First test: ‘‘range1NULLCombineIgnore()’ uses a null value as the first argument, with exampleRange being the first, and the expected result of no altering being performed on the exampleRange object occurs. The expected return value is true. 
* Second test: ‘‘range2NULLCombineIgnore()’ uses a null value as the second argument, with exampleRange being the first, and the expected result of no altering being performed on the exampleRange object occurs. The expected return value is true. 
* Third test: ‘rangeCombineIgnore()’ creates two new Range objects, first with a lower and upper bound 0 and 2, second with a lower and upper bound of -1 and 2. The method is applied to exampleRange using the first newly created object as the second argument, and the expected return value is true as the resulting range for exampleRange should now match the second newly created object.  
* Fourth test: ‘testNaNBoth()’ creates two new Range objects with the upper and lower bounds of both objects created using ‘Double.NaN’. The method is applied to the first of these objects and the expected return value is true, as the resulting range should be null. 
* Fifth test: ‘testNaNnull1()’ creates a new Range object with lower and upper bounds being created with ‘Double.NaN’. Using this object as the first argument and a null value as the second, the ‘expandToInclude’ method is applied and the expected return value is true as the resulting range matches the expected ‘null’ value for the range.  
* Sixth test: ‘testNaNnull2()’  creates a new Range object with lower and upper bounds being created with ‘Double.NaN’. Using this object as the second argument and a null value as the first, the ‘expandToInclude’ method is applied and the expected return value is true as the resulting range matches the expected ‘null’ value for the range.  


<h3>8. expandToInclude(Range range1, Range range2)</h3>

‘expandToInclude’ receives aRange object and a double value then returns a range that includes all the values specified in the range and the specified value.

* First test: ‘rangeExpandNull()’ creates a new Range object with a lower and upper bound both of 2. A null value is passed as the Range object to be expanded. The resulting range is not expanded and the expected output is true as the newly created Range object was not altered. 
* Second test: ‘rangeExpandUpper()’ creates a new Range object with a lower and upper bound of -1 and 2. Then exampleRange is expanded by a value of 2, matching the newly created Range object and producing an expected output of true. 
* Third test: ‘rangeExpandLower()’ creates a new Range object with a lower and upper bound of -2 and 1. Then exampleRange is expanded by a value of -2, matching the newly created Range object and producing an expected output of true. 
* Fourth test: ‘rangeNoExpand()’ creates a new Range object with a lower and upper bound of -1 and 1. Then exampleRange is expanded by a value of 0, matching the newly created Range object and producing an expected output of true. 

<h3>9. expand(Range range, double lowerMargin, double upperMargin)</h3>

‘Expand’ receives a Range object and two other double values specifying both an upper and lower margin to expand the existing range of the Range object by, then proceeds to expand the range by the specified values. 

* First test: ‘rangeExpansion()’ creates a new Range object with a lower and upper bound of -3 and 3. ‘Expand’ is then applied to exampleRange with a positive value for both the upper and lower margins to be applied to the upper and lower bounds of the exampleRange object. The expected return value is true as the example range should have a range matching that of the newly created object. 
* Second test: ‘rangeExpansionFlip()’ creates two new Range objects, first with a lower and upper bound of 10 and 20, and second with a lower and upper bound both with a value of 25.5. A negative value and a double value are then used as arguments for the ‘expand’ method. The expected return value is true as the example range should have a range matching that of the newly created object. 

<h3>10. shift(Range base, double delta)</h3>

’shift’ receives a Range object and a double value to shift the existing range by. It may also receive a boolean value to indicate if the range is allowed to cross over zero as a result of the shift. 

* First test: ‘rangeShift()’ creates a new Range object with a lower and upper bound of 0 and 2. exampleRange is then used with an indicated shift factor of 1 alongside the shift’ function. The expected return value is true as exampleRange ‘s range should now be moved by a value of 1 in the positive direction for both upper and lower bounds. 
* Second test: ‘rangeShiftZeroCross()’ creates a new Range object with a lower and upper bound of 1 and 3. exampleRange is then used with an indicated shift factor of 2 alongside the shift’ function. The expected return value is true as exampleRange ‘s range should now be moved by a value of 2 in the positive direction for both upper and lower bounds. A boolean value of true was also passed as an argument creating a situation where zero-crossing is acceptable for the bound shifting.
* Third test: ‘rangeShiftNoZeroCross()’ creates two new Range objects, first with a lower and upper bound both of 0, and second with both upper and lower bounds of 2. exampleRange is then used with an indicated shift factor of 2 alongside the shift’ function. The expected return value is true as exampleRange ‘s range should now be moved by a value of 2 in the positive direction for both upper and lower bounds. A boolean value of false was also passed as an argument creating a situation where zero-crossing is not acceptable for the bound shifting.

<h3>11. scale(Range base, double factor)</h3>

‘scale’ receives a Range object and double value then scales the range by the specified factor.

* First test: ‘scaleException()’ tests to see whether or not the proper exception is thrown when an invalid argument is passed to be used as the expanding factor. A negative value is passed, and the exception is expected to be thrown.
* Second test: ‘rangeScale()’ creates a new Range object with a lower and upper bound of -4 and 4. The new Range object is used to compare the result of applying the ‘scale’ method to the exampleRange object after indicating for it to be scaled by a factor of 4. The expected return value is true. 

<h3>12. equals(Object obj)</h3>

‘equals’ receives an object and tests the object for equality with an arbitrary object. 

* First test: ‘equalsNotObject()’ creates a double value to be used when the example Range object called exampleRange has the ‘equals’ function applied to it. The expected return value is false.
* Second test: ‘equalsNotUpper()’ creates a new Range object with a lower and upper bound of -2 and 1 in order to test how different negative values associated with exampleRange are considered following the application of ‘equals’. The expected return value is false, the two objects are not equivalent. 
* Third test: ‘equalsNotLower()’ creates a new Range object with a lower and upper bound of -1 and 2 in order to test how different negative values associated with exampleRange are considered following the application of ‘equals’. The expected return value is false, the two objects are not equivalent. 

<h3>13. hashCode()</h3>

‘Hashcode’ returns a hashcode. 

* First test: ‘hashTest()’ creates an integer value to compare with the hashcode returned by applying the ‘hashCode’ function to the example Range object called exampleRange. The expected return value is true. 


<h3>14. toString()</h3>

‘toString’ returns a string in representation of this Range. 

* First Test: ‘stringTest()’ creates a string to compare with the result of applying the ‘toString’ method on the example Range object called exampleRange. The expected return value is true.

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
<img width="1086" alt="Screen Shot 2023-03-02 at 10 19 39 AM" src="https://user-images.githubusercontent.com/101214266/222503705-68f8bd31-86ef-4fab-b119-1d6f400f889c.png">
<img width="1089" alt="Screen Shot 2023-03-02 at 10 20 06 AM" src="https://user-images.githubusercontent.com/101214266/222503808-a809d7bd-a302-4a08-b136-02afc67f6f63.png">
<img width="1097" alt="Screen Shot 2023-03-02 at 10 20 24 AM" src="https://user-images.githubusercontent.com/101214266/222503896-819f50f4-8354-419b-ae0f-293b35901b15.png">


## __Statement:__
<img width="708" alt="Screen Shot 2023-03-02 at 10 21 14 AM" src="https://user-images.githubusercontent.com/101214266/222504102-2dec652b-b2f6-42cd-accb-394f04a83128.png">


## __Branch:__
<img width="690" alt="Screen Shot 2023-03-02 at 10 22 00 AM" src="https://user-images.githubusercontent.com/101214266/222504293-ad63ef89-fa49-4220-8d20-73b1ea70925f.png">


## __Method:__
<img width="700" alt="Screen Shot 2023-03-02 at 10 22 24 AM" src="https://user-images.githubusercontent.com/101214266/222504396-56bb82a2-4d2e-48ae-80cf-68236042668f.png">



For Range, the new Statement coverage was 90.8%. This number could not be 100% as certain functions throw an IllegalArgumentException, when they are passed a range with a lower greater than the upper, but it is impossible to pass them a range where lower is greater than upper because of the error checking in the constructor, so these lines cannot be covered. The Branch coverage was 84.1%, a massive 71.9% increase from the first implementation of the unit testing. Since EclEmma cannot analyze for condition coverage, we looked at the Method coverage instead, which is 100%, as all methods were accounted for.


# 6 Pros and Cons of coverage tools used and Metrics you report

Utilizing EclEmma allowed us to view the coverages our test cases provided. Its robust ability to function with mockery objects permitted us to retain much of our original test cases, and expand upon features through white-box testing. The coverage data is useful in understanding test case effectiveness. It was easy to use, clear; and useful. However, EclEmma lacks coverage options, forcing us to analyze method coverage as opposed to condition coverage. 

# 7 A comparison on the advantages and disadvantages of requirements-based test generation and coverage-based test generation.

<h3>Requirements-Based</h3>

Requirements based testing utilizes specific requirements in order to design the tests. Developers can achieve a higher probability of detecting defects, ensure requirements are met, and can help reduce the number of tests needed. However obtaining the specific requirements is difficult and time consuming. It can also be challenging to maintain, as the test suite may fluctuate frequently.

<h3>Coverage-Based</h3>

Coverage based testing analyzes the coverages of each code path, allowing developers to measure the quality of the test suite and can help detect defects that might be missed. However, not all defects may be found, and it can be time-consuming to develop and maintain redundant test cases. Additionally, some coverage may not be feasibly tested.

# 8 A discussion on how the team work/effort was divided and managed

<h3> Brenek & Ben</h3>

Brenek primarily worked on implementing the new test cases and managing the coverage details, while also helping with the test plan and diagrams. Ben primarily worked on the test plan and the dataflow diagrams, while also helping to implement the test through peer programming. 

<h3> Jack & Arion</h3>

Jack implemented the new test cases and managed the coverage details. He also worked on the dataflow diagrams above. Arion created the test plan and aided Jack where possible through peer programing.

# 9 Any difficulties encountered, challenges overcome, and lessons learned from performing the lab

<h3> Brenek & Ben</h3>
One large diffucutly in Range was getting the statement coverage higher than 86% statement coverage. In functions such as getLowerBound() and getUpperBound(), there is error checking for a range where lower is greater than upper even though these functions cannot be passed a range where these conditions are met. Additionally, there is functions that check for a NaN, that we did not know how to test. We overcame this challenge by researching NaN and discovering in java there is Double.NaN which allowed us to test the functions dealing with NaN and get our statement coverage over 90%.

<h3> Jack & Arion</h3>

One large difficulty in DataUtilities was the inability to achieve higher than 88.5% Statement coverage, as there was an infinite loop in the code. This was discovered by looking at the error output from the mocking, which lead us to realize that the error was present and we could not increase our coverage in this way without breaking our code. We resolved this issue by focusing our coverage onto other parts of the code that were not as broken.

# 10 Comments/feedback on the lab itself

We all found this lab to be more interesting than the ones before. We also felt as though this lab was very good practice for the approaching midterm, as it gave us plenty of knowledge with not only unit testing and coverage, but also DU pairs and data flow charts.
