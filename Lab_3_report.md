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
![img]()

- Code before change:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
}
```

- Code after change:
```
static void reverseInPlace(int[] arr) {
  int left = 0;
  int right = arr.length - 1;
  while(left < right){
    int temp = arr[left];
    arr[left] = arr[right];
    arr[right] = temp;
    left++;
    right--;
  }
}
```
- Why does the fix address the issue?
   - The issue of the original implementation is: If we have [1,2,3,4,5], the output of it is [5,4,3,4,5], which is wrongly overwriting, and while iterating, the original value have lost.
   - The fix addresses this issue, letting one variable to iterate from the beginning and the other one from the back, meet at the middle.
   - It swaps elements during each iteration.

- Show each example as a code block that shows the command and its output, and write a sentence or two about what it’s doing and why it’s useful.
  1. grep -v
```
NealC@LAPTOP-R81VOUDE MINGW64 /d/java_code/docsearch (main)
$ grep -v ".txt" find-results.txt
technical/biomed
```
For example: in this case, it only shows you the lines that doesn't have ".txt", which is technical/biomed. Prints lines not matching criteria (inverse search)

  2. grep -c
```
NealC@LAPTOP-R81VOUDE MINGW64 /d/java_code/docsearch (main)
$ grep -v -c ".txt" find-results.txt 
1
```
Prints count of lines with matching criteria. In this case, only **1** line doesn't have".txt", so it prints 1.


