# Lab Report 3
## 1. Part 1: Bug in reversed Method in ArrayExample.java
**1.　Failure-Inducing Input**
```
@Test
public void testReversedFail() {
  int[] input1 = {1};
  assertArrayEquals(new int[]{1}, ArrayExamples.reversed(input1));
}
```
**2.　Pass-Inducing Input**
```
@Test
public void testReversedPass() {
  int[] input1 = {};
  assertArrayEquals(new int[]{}, ArrayExamples.reversed(input1));
}
```
**3.　Symptom**
```
There was 1 failure:
1) testReversedFail(ArrayTests)
arrays first differed at element [0]; expected:<1> but was:<0>
at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
at org.junit.Assert.internalArrayEquals(Assert.java:534)
at org.junit.Assert.assertArrayEquals(Assert.java:418)
at org.junit.Assert.assertArrayEquals(Assert.java:429)
at ArrayTests.testReversedFail(ArrayTests.java:21)
... 30 trimmed
Caused by: java.lang.AssertionError: expected:<1> but was:<0>
at org.junit.Assert.fail(Assert.java:89)
at org.junit.Assert.failNotEquals(Assert.java:835)
at org.junit.Assert.assertEquals(Assert.java:120)
at org.junit.Assert.assertEquals(Assert.java:146)
at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
... 36 more

FAILURES!!!
```
**4. Bug**
- Before
```
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = newArray[arr.length - i - 1];
  }
  return arr;
}
```
- After
```
static int[] reversed(int[] arr) {
  int[] newArray = new int[arr.length];
  for(int i = 0; i < arr.length; i += 1) {
    newArray[i] = arr[i];
  }
  for(int i = 0; i < arr.length; i += 1) {
    arr[i] = newArray[arr.length - i - 1];
  }
  return arr;
}
```
**Explanation**
Initially, the second for statement was copying elements from an empty array newArray. Hence, the output was always going to be an empty array. In order to fix this, newArray must be a copy of the original arr, which is why the first for statement is added. Now, the second for statment refers to the elements of original arr in reverse order, giving the output we want.
## 2. Part 2: Researching Commands: grep
> The working directory for part 2 is /technical

**1. -i**

**Input 1:** 
```
grep -i "further" biomed/1471-5945-2-13.txt
```
**Output 1:**
```
Additional data #3). TGFβ1 further induced the expression
outside tension. Furthermore, persisting tension in the
further limited by the PP fibroblast requirement for higher
```
**Input 2:** 
```
grep -i "THEI" biomed/1471-2180-3-5.txt
```
**Output 2:**
```
induction of TRAIL by Theiler's murine encephalomyelitis
their ability to induce inflammatory responses. The two
``` 
**Explanation**

-i ignores the difference in uppercase and lowercase letters when looking for the lines with the given string. This is helpful in cases where the string you want to look for are capitalized due to some reasons.

**2. -c**

**Input 1:** 
```
grep -c " " plos/journal.pbio.0020001.txt
```
**Output 1:**
```
230
```
**Input 2:** 
```
grep -c "hi" 911report/*.txt
```
**Output 2:**
```
911report/chapter-1.txt:253
911report/chapter-10.txt:101
911report/chapter-11.txt:179
911report/chapter-12.txt:193
911report/chapter-13.1.txt:132
911report/chapter-13.2.txt:198
911report/chapter-13.3.txt:199
911report/chapter-13.4.txt:603
911report/chapter-13.5.txt:608
911report/chapter-2.txt:232
911report/chapter-3.txt:592
911report/chapter-5.txt:441
911report/chapter-6.txt:351
911report/chapter-7.txt:513
911report/chapter-8.txt:183
911report/chapter-9.txt:373
911report/preface.txt:26
``` 
**Explanation**

-c returns only the count of lines with the given string, not the lines themselves. This is helpful when you want to just know how many lines with the given string are there.

**3. -l**

**Input 1:** 
```
grep -l "individual" biomed/1471-210*.txt
```
**Output 1:**
```
biomed/1471-2105-1-1.txt
biomed/1471-2105-2-1.txt
biomed/1471-2105-2-8.txt
biomed/1471-2105-2-9.txt
biomed/1471-2105-3-12.txt
biomed/1471-2105-3-14.txt
biomed/1471-2105-3-16.txt
biomed/1471-2105-3-17.txt
biomed/1471-2105-3-18.txt
biomed/1471-2105-3-2.txt
biomed/1471-2105-3-22.txt
biomed/1471-2105-3-23.txt
biomed/1471-2105-3-24.txt
biomed/1471-2105-3-26.txt
biomed/1471-2105-3-28.txt
biomed/1471-2105-3-3.txt
biomed/1471-2105-3-30.txt
biomed/1471-2105-3-34.txt
biomed/1471-2105-3-37.txt
biomed/1471-2105-3-38.txt
biomed/1471-2105-3-4.txt
biomed/1471-2105-3-6.txt
biomed/1471-2105-4-13.txt
biomed/1471-2105-4-24.txt
biomed/1471-2105-4-25.txt
biomed/1471-2105-4-26.txt
biomed/1471-2105-4-27.txt
biomed/1471-2105-4-31.txt
```
**Input 2:** 
```
grep -l "government" government/About_LSC/commission_report.txt
```
**Output 2:**
```
government/About_LSC/commission_report.txt
``` 
**Explanation**

-l returns the name of the files with lines with the given string. This is helpful when you want to just know which file has the given string.

**4. -v**

**Input 1:** 
```
grep -v "a" biomed/rr37.txt
```
**Output 1:**
```
Introduction
        22].



          interviews (
          study findings.
          (
          n = 371) with registered subjects (

          n = 242), subjects without complete
          follow-up interviews (
          P = 0.10, respectively). There were




          from 0 to 28, with higher scores reflecting more severe





        Results





          2.5; 95% CI, 1.1-5.5).


          systemic corticosteroid score (OR, 1.7 per 5-point score
          severity.
          (OR, 1.2; 95% CI, 1.03-1.4).



        Discussion
        3-month follow-up [ 14]. In the present study, however,
        results.
        smoking.
        Consistent with this finding, Levin
        30].


        Conclusion



          telephone interview.


          $75,000). To convert to specific income levels, the
```
**Input 2:** 
```
grep -v " " plos/pmed.0010056.txt
```
**Output 2:**
```

``` 
**Explanation**

-v returns the lines without the given string. This is helpful since for some short strings, the output could be a lot and hard to understand, making it is easier to look for ones that does not include the given string and take that those that did not come up in the output do include the given string.
