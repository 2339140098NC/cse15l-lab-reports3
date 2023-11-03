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
   source: [https://www.geeksforgeeks.org/grep-command-in-unixlinux/]
  ```
  NealC@LAPTOP-R81VOUDE MINGW64 /d/java_code/docsearch (main)
  $ grep -v ".txt" find-results.txt
  technical/biomed
  ```
  ```
  NealC@LAPTOP-R81VOUDE MINGW64 /d/java_code/docsearch (main)
  $ grep -v " " find-results.txt
  technical/biomed
  technical/biomed/1468-6708-3-1.txt
  technical/biomed/1468-6708-3-10.txt
  technical/biomed/1468-6708-3-3.txt
  technical/biomed/1468-6708-3-4.txt
  technical/biomed/1468-6708-3-7.txt
  technical/biomed/1471-2091-2-10.txt
  technical/biomed/1471-2091-2-11.txt
  technical/biomed/1471-2091-2-12.txt
  technical/biomed/1471-2091-2-13.txt
  technical/biomed/1471-2091-2-16.txt
  technical/biomed/1471-2091-2-5.txt
  ...
  ```
  For example: in this case, it only shows you the lines that doesn't have ".txt", which is technical/biomed. Prints lines not matching criteria (inverse search), we can use it when we want to seach for everything else except certain line with certain info that we don't want to search for

2. grep -c
  source: [https://www.geeksforgeeks.org/grep-command-in-unixlinux/]
  ```
  NealC@LAPTOP-R81VOUDE MINGW64 /d/java_code/docsearch (main)
  $ grep -v -c ".txt" find-results.txt 
  1
  ```
  ```
  NealC@LAPTOP-R81VOUDE MINGW64 /d/java_code/docsearch (main)
  $ grep -c ".txt" find-results.txt
  837
  ```

  Prints count of lines with matching criteria. In this case, only **1** line doesn't have".txt", so it prints 1. Can help to know how many lines contains

3. grep -w
   source: [https://www.geeksforgeeks.org/grep-command-in-unixlinux/]
  ```
NealC@LAPTOP-R81VOUDE MINGW64 /d/java_code/docsearch (main)
$ grep -w 2121 find-results.txt 
technical/biomed/1471-2121-1-2.txt
technical/biomed/1471-2121-2-1.txt
technical/biomed/1471-2121-2-10.txt
technical/biomed/1471-2121-2-11.txt
technical/biomed/1471-2121-2-12.txt
technical/biomed/1471-2121-2-15.txt
technical/biomed/1471-2121-2-18.txt
technical/biomed/1471-2121-2-21.txt
technical/biomed/1471-2121-2-22.txt
technical/biomed/1471-2121-2-3.txt
technical/biomed/1471-2121-2-6.txt
technical/biomed/1471-2121-3-10.txt
technical/biomed/1471-2121-3-11.txt
technical/biomed/1471-2121-3-12.txt
technical/biomed/1471-2121-3-13.txt
technical/biomed/1471-2121-3-15.txt
technical/biomed/1471-2121-3-16.txt
technical/biomed/1471-2121-3-18.txt
technical/biomed/1471-2121-3-19.txt
technical/biomed/1471-2121-3-2.txt
technical/biomed/1471-2121-3-21.txt
technical/biomed/1471-2121-3-22.txt
technical/biomed/1471-2121-3-25.txt
technical/biomed/1471-2121-3-30.txt
technical/biomed/1471-2121-3-4.txt
technical/biomed/1471-2121-3-6.txt
technical/biomed/1471-2121-3-8.txt
technical/biomed/1471-2121-4-1.txt
technical/biomed/1471-2121-4-2.txt
technical/biomed/1471-2121-4-3.txt
technical/biomed/1471-2121-4-4.txt
technical/biomed/1471-2121-4-5.txt
technical/biomed/1471-2121-4-6.txt
  ```
```
NealC@LAPTOP-R81VOUDE MINGW64 /d/java_code/docsearch (main)
$ grep -w rr74 find-results.txt 
technical/biomed/rr74.txt
```
It prints whole word matches, it's useful when you know the filename but don't know where it is in the file.

4. grep -o
source: [https://www.geeksforgeeks.org/grep-command-in-unixlinux/]
```
NealC@LAPTOP-R81VOUDE MINGW64 /d/java_code/docsearch (main)
$ grep -o rr74 find-results.txt 
rr74
```
```
NealC@LAPTOP-R81VOUDE MINGW64 /d/java_code/docsearch (main)
$ grep -o rr196 find-results.txt 
rr196
```
Display only the matched pattern, it's not very useful to be honest.




