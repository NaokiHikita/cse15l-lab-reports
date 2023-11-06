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
Initially, the second for statement was copying elements from an empty array newArray. Hence, the output was always going to be an empty array. In order to fix this, newArray must be a copy of the original arr, which is why the first for statement is added. Now, the second for statment refers to the elements of original arr in reverse order, giving the output we want.
## 2. Part 2
