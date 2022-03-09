# SENG-637 Assignment 3

**Topic** - Code Coverage, Adequacy Criteria and Test Case Correlation

## Table of Contents

- [Introduction](#introduction)
- [Video demo](#video-demo)
- [Detailed description of unit test strategy](#detailed-description-of-unit-test-strategy)
- [Test cases developed](#test-cases-developed)
- [Division of team work](#division-of-team-work)
- [Difficulties, challenges, and lessons learned](#difficulties-challenges-and-lessons-learned)
- [Comments and feedback](#comments-and-feedback)
- [Contributors](#contributors)

## Introduction

Text…

## Video demo

Link to the video demonstration of testing is _TBA_.

## Manual data flow coverage

### 1. `Range.intersects(double b0, double b1)`

![DFG_Intersects.png](drafts/DFG_Intersects.png)

#### Defs, uses, and du-pairs

|               |                                |
| ------------- | ------------------------------ |
| **defs**:     | def(1) = {b0, b1}              |
| **uses**:     | use(2) = {b0, this.lower}      |
|               | use(3) = {b1, this.lower}      |
|               | use(5) = {b0, this.upper}      |
|               | use(6) = {b0, b1}              |
| **du-pairs**: | for b0: (1, 2), (1, 5), (1, 6) |
|               | for b1: (1, 3), (1, 6)         |

#### DU-pair coverage calculation per test case

| Variable | Def at node (n) | dcu(v, n) | dpu(v, n)                                        |
| -------- | --------------- | --------- | ------------------------------------------------ |
| b0       | 1               | {}        | {(2, 3), (2, 5), (5, 6), (5, 7), (6, 4), (6, 7)} |
| b1       | 1               | {}        | {(3, 4), (3, 7), (6, 4), (6, 7)}                 |
|          | Total           | CU = 0    | PU = 10                                          |

| Test case                      | DU path         | DU-pairs covered       | PUc                    | All-uses coverage % |
| ------------------------------ | --------------- | ---------------------- | ---------------------- | ------------------- |
| `intersectsWithInputBLBAndLB`  | [1, 2, 3, 7]    | (1, 2), (1, 3)         | (2, 3), (3, 7)         | 20%                 |
| `intersectsWithInputBLBAndALB` | [1, 2, 3, 4]    | (1, 2), (1, 3)         | (2, 3), (3, 4)         | 20%                 |
| `intersectsWithInputBLBAndAUB` | [1, 2, 3, 4]    | (1, 2), (1, 3)         | (2, 3), (3, 4)         | 20%                 |
| `intersectsWithInputLBAndALB`  | [1, 2, 3, 4]    | (1, 2), (1, 3)         | (2, 3), (3, 4)         | 20%                 |
| `intersectsWithInputLBAndUB`   | [1, 2, 3, 4]    | (1, 2), (1, 3)         | (2, 3), (3, 4)         | 20%                 |
| `intersectsWithInputNOMAndNOM` | [1, 2, 5, 6, 4] | (1, 2), (1, 5), (1, 6) | (2, 5), (5, 6), (6, 4) | 40%                 |
| `intersectsWithInputBUBAndUB`  | [1, 2, 5, 6, 4] | (1, 2), (1, 5), (1, 6) | (2, 5), (5, 6), (6, 4) | 40%                 |
| `intersectsWithInputUBAndAUB`  | [1, 2, 5, 7]    | (1, 2), (1, 5)         | (2, 5), (5, 7)         | 20%                 |
| `intersectsWithInputMINAndAUB` | [1, 2, 5, 6, 4] | (1, 2), (1, 5), (1, 6) | (2, 5), (5, 6), (6, 4) | 40%                 |
| `intersectsWithInputBLBAndMAX` | [1, 2, 3, 4]    | (1, 2), (1, 3)         | (2, 3), (3, 4)         | 20%                 |
| `intersectsWithInput0And0`     | [1, 2, 5, 6, 4] | (1, 2), (1, 5), (1, 6) | (2, 5), (5, 6), (6, 4) | 40%                 |
| `intersectsWithInputNaNAnd1`   | [1, 2, 5, 7]    | (1, 2), (1, 5)         | (2, 5), (5, 7)         | 20%                 |

### 2. `DataUtilities.calculateColumnTotal(Values2D data, int column, int[] validRows)`

![DFG_CalculateColumnTotal.png](drafts/DFG_CalculateColumnTotal.png)

#### Defs, uses, and du-pairs

|               |                                          |
| ------------- | ---------------------------------------- |
| **defs**:     | def(1) = {data}                          |
|               | def(1) = {column}                        |
|               | def(2) = {total}                         |
|               | def(3) = {rowCount}                      |
|               | def(4) = {r}                             |
|               | def(7) = {n}                             |
|               | def(9) = {total}                         |
|               | def(10) = {r}                            |
| **uses**:     | use(5) = {r}                             |
|               | use(5) = {rowCount}                      |
|               | use(6) = {total}                         |
|               | use(8) = {n}                             |
|               | use(9) = {n}                             |
|               | use(9) = {total}                         |
|               | use(10) = {r}                            |
| **du-pairs**: | for data: (1, 3), (1, 7)                 |
|               | for column: (1,7)                        |
|               | for total: (2, 6), (2, 9), (9,9)         |
|               | for rowCount: (3, 5)                     |
|               | for r: (4, 5), (4, 7), (4, 10), (10, 10) |
|               | for n: (7, 8), (7, 9)                    |


#### DU-pair coverage calculation per test case

| Variable | Def at node (n) | dcu(v, n) | dpu(v, n)         |
| -------- | --------------- | --------- | ----------------- |
| data     | 1               | {3, 7}    | {}                |
| column   | 1               | {7}       | {}                |
| total    | 2               | {9}       | {}                |
| total    | 9               | {9}       | {}                |
| rowCount | 3               | {}        | {(5, 6), (5, 7)}  |
| r        | 4               | {7, 10}   | {(5, 6), (5, 7)}  |
| r        | 10              | {10}      | {}                |
| n        | 7               | {9}       | {(8, 9), (8, 10)} |
|          | Total           | CU = 9    | PU = 6            |

#### DU-pair coverage in test cases

| Test case                                        | DU-pair coverage |
| ------------------------------------------------ | ---------------- |
| `calculateColumnTotalAllRowsFirstColumn`         |                  |
| `calculateColumnTotalAllRowsMiddleColumn`        |                  |
| `calculateColumnTotalAllRowsLastColumn`          |                  |
| `calculateColumnTotalWithMaxValueAndFirstColumn` |                  |
| `calculateColumnTotalWithMinValueAndFirstColumn` |                  |
| `calculateColumnTotalWithMaxValueColumn`         |                  |
| `calculateColumnTotalWithMinValueColumn`         |                  |
| `calculateColumnTotalWithSumOf0AndFirstColumn`   |                  |

## A detailed description of the testing strategy for the new unit test

With the testing strategy in this assignment, we will first run the coverage tool (EclEmma) on the test cases that we developed from assignment 2 and analyze the coverage first with respect to the Lines, Branches and Method metrics. Afterwards, we will then designed specific test cases to cover the lines,branches and/or methods that are not covered from our previous test cases developed in assignment 2.

Lastly, coverage tool will run with these new test cases to ensure that the coverage metrics are above the expected requirements.

## A high level description of five selected test cases you have designed using coverage information, and how they have increased code coverage

Text…

## A detailed report of the coverage achieved of each class and method (a screen shot from the code cover results in green and red color would suffice)
Range coverage Before  
![image](Report_Images/Range_Line_Coverage_Before.PNG)  
![image](Report_Images/Range_Branch_Coverage_Before.PNG)  
![image](Report_Images/Range_Method_Coverage_Before.PNG)  
Data Utilities coverage Before  
![image](Report_Images/DataUtilities_Line_Coverage_Before.PNG)  
![image](Report_Images/DataUtilities_Branch_Coverage_Before.PNG)  
![image](Report_Images/DataUtilities_Method_Coverage_Before.PNG) 

## Pros and Cons of coverage tools used and Metrics you report

In this report, we will be using EclEmma to report the coverage metrics. EclEmma only supports statement and branch coverage, but does not support condition coverage. 
Other tools have been experimented but we cannot get the condition coverage to work. For example, CodeCover do have condition coverage, but it seems that it is discontinued from support.

When we run CodeCover on the current version of eclipse, it will produce the following error:
Plug-in "org.codecover.eclipse" was unable to instantiate class "org.codecover.eclipse.junit.JUnitLaunchConfigurationDelegate".org/eclipse/osgi/framework/internal/core/BundleHost 

Upon researching this issue on stackoverflow, it seems that only Eclipse Kepler can be used with CodeCover.
We have also attempted to install Eclipse Kepler on another system to test CodeCover, but unfortunately we have multiple issues running the jfreechart code in that version of Eclipse. 
  
JaCoco has basically the same featureset as EclEmma, there are no differences and thus EclEmma is used.
As for Clover, we have not been able to obtain the 30-day evaluation key successfully from my.atlassian.com. However, given that it is a paid tool, we believe that EclEmma is still a better solution as it is more user-friendly to install and does not require a key while providing similar functionality.
Coverlipse (http://coverlipse.sourceforge.net/) and Cobertura (http://cobertura.github.io/cobertura/) had not been tested.
Thus, going forward, the tests made in this report will be using EclEmma.


## A comparison on the advantages and disadvantages of requirements-based test generation and coverage-based test generation.
### Requirements-based test generation
- Advantages
    - More representative of actual use cases as a user would read Javadoc
    - Test cases are not biased by looking at the code
- Disadvantages
    - No way to verify test coverage 
    - Planning must be more thorough to ensure all cases are tested
    - Test cases may test the same paths multiple times as testers are unsure of the code

## Division of team work

### 3.2 Manual data flow coverage
This section was worked on togeater
### 3.3 TEST SUITE DEVELOPMENT

Each of the four testers will increase coverage of the following methods.

| API method                                                 | Tester                   |
| ---------------------------------------------------------- | ------------------------ |
| `Range.isNaNRange()`                                       | Bhavyai Gupta            |
| `Range.shift(Range, double, boolean)`                      | None (Already 100%)      |
| `Range.intersects(double, double)`                         | Michael Man Yin Lee      |
| `Range.expandToInclude(Range, double)`                     | Drew Burritt             |
| `Range.combineIgnoringNaN(Range, Range)`                   | Bhavyai Gupta            |
| `DataUtilities.calculateRowTotal(Values2D, int)`           | Michael Man Yin Lee      |
| `DataUtilities.calculateRowTotal(Values2D, int, int[])`    | Bhavyai Gupta            |
| `DataUtilities.calculateColumnTotal(Values2D, int)`        | Michael Man Yin Lee      |
| `DataUtilities.calculateColumnTotal(Values2D, int, int[])` | Drew Burritt             |
| `DataUtilities.getCumulativePercentages(KeyedValues)`      | None (Already 100%)      |


## Difficulties, challenges, and lessons learned

Text…

## Comments and feedback

1. This assignment has given us a great opportunity in learning how to make sure the test cases we write are complete and cover most of the source code effectively.

2. This assignment gave us a chance to review our assignment 2 work and see how well we did with black box testing

3. EclEmma was used as the code coverage tool, which is already available Eclipse as an installed plugin.

4. The assignment description document [`Assignment3.md`](Assignment3.md) is very detailed and comprehensive, and it was easy to follow.

## Contributors

We are group 5, and below are the team members

- [Bhavyai Gupta](https://github.com/zbhavyai)
- [Drew Burritt](https://github.com/dburritt)
- [Michael Man Yin Lee](https://github.com/mlee2021)
- [Okeoghenemarho Obuareghe](https://github.com/oobuareghe)
