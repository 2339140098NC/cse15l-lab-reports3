# Lab 3 Report
- A failure-inducing input for the buggy program
```
@Test
public void LongArrayTestRIP(){
  int[] input1 = {1,2,3,4,5};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{5,4,3,2,1}, input1);
}
```


- An input that doesn’t induce a failure
```
@Test 
public void testReverseInPlace() {
  int[] input1 = { 3 };
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{ 3 }, input1);
}
```

-The symptom, as the output of running the tests: 
