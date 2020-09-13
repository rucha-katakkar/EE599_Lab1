# EE599_Lab1

# HW1 EE599 - Computing Principles for Electrical Engineers

- Plesae clone the repository, edit [README.md](README.md) to answer the questions, and fill up functions to finish the hw.
- For non-coding quesitions, you will find **Answer** below each question. Please write your answer there.
- For coding questions, please make sure that your code can run ```blaze run/test```. In this homework, you will need to fill up [cpplib.cc](src/lib/cpplib.cc), [q5_student_test.cc](tests/q5_student_test.cc), [q6_student_test.cc](tests/q6_student_test.cc), [q7_student_test.cc](tests/q7_student_test.cc) for question  5, 6, 7.
- For submission, please push your answers to Github before the deadline.
- Deadline: Friday, September 4th by 6:30 pm
- Total: 120 points. 100 points is considered full credit.

## Question 1 (10 Points. Medium)

Use proof by contradiction to prove that the FindMax function always finds the maximum value in the input vector.

```cpp
int FindMax(std::vector<int> &inputs) {
   if (inputs.size() == 0) {
       return -1;
   }
   int result = INT32_MIN;
   for (auto n : inputs) {
       if (n > result) {
           result = n;
       }
   }
   return result;
}
```

Answer:

Assume that the result returned value is smaller than the max value in the input array. We are checking each element in input is greater than the returned value "result". So if we are not getting the max value in the array, it would either mean following 2 conditions:
1) we are not checking all the elements in the input array => this is false since the for statement (auto n: inputs') by definition should check all elements in input array
2) returned value is not the max value in the array => this is false again since the if condition checks if the element in the input array is > result and makes result =n if n is greater. This would mean result should always return the max value in the input array.
Lets take a few examples to prove that this is not true:

1)  inputs=[2,5,3,1]
1st iteration would check if 2> int32_min => true => result = 2
2nd iteration would check if 5> 2 => true => result = 5
3rd iteration would check if 5> 2 => true => result = 5


## Question 2 (20 Points. Medium)

What is the time complexity of the below functions?

```cpp
int Example1(int n) {
   int count = 0;
   for (int i = n; i > 0; i /= 2) {
       for (int j = 0; j < i; j++) {
           count += 1;
       }
   }
   return count;
}
```

Answer:
O(log^2(n))
outer for loop will give O(log(n)) and innter loop will iterate for each i in tge same order so O(log(n)) again 


```cpp
void Example2(int a = 0, int n) {
   int i = n;
   while (i > 0) {
       a += i;
       i /= 2;
   }
}
```

Answer: O(log(n)) since iterates over a single loop i/=2 times.

```cpp
void Example3(int n) {
   int count = 0;
   for (int i=n/2; i<=n; i++) {
       for (int j=1; j<=n; j = 2 * j) {
           for (int k=1; k<=n; k = k * 2) {
               count++;
           }
       }
   }
}
```

Answer: 
O((n^2)logn) 
inner two loops give O(n) for each loop, outer gives O(logn)

```cpp
void Example4(int n) {
   int count = 0;
   for (int i=0; i<n; i++)
       for (int j=i; j< i*i; j++)
           if (j%i == 0)
           {
               for (int k=0; k<j; k++)
                   cout<<"*";
           }
}
```

Answer: 
O(n^5)
2 loops n^2 order, => n^4 and one loop O(n)
## Question 3 (10 Points. Easy)

What does it mean when we say that the Merge Sort (MS) algorithm is asymptotically more efficient than the Bubble Sort (BS) algorithm? Support your choice with an explanation.

1. MS will always be a better choice for small inputs
2. MS will always be a better choice for large inputs
3. BS will always be a better choice for small inputs
4. MS will always be a better choice for all inputs

Answer: 2. Merge sort splits the array in two halves and checks the right element with the left element for both halves and keeps sorting accordingly giving a time compexity of O(nlogn), O(logn) for iterating i/2 times and O(n) for sorting the n elements, where as bubble sort comares each element with the one next to it nd sorts gicing a time complexity of O(n^2).
for smaller arrays say 3 size, bubble sort would be more efficiet as you wont add the order of splitting the array, just check for i= 0:3 . 
## Question 4 (10 Points. Easy)

Create an account on GitHub and Stack Overflow and paste the link to your profile.

Answer:

GitHub profile link: https://github.com/rucha-katakkar

Stack Overflow profile link: https://meta.stackexchange.com/users/849401/rucha-katakkar

## Question 5 (15 Points. Easy)

Write a simple function ```std::string CPPLib::PrintIntro()``` in [cpplib.cc](src/lib/cpplib.cc) to print your name, email, and any information about you that you want (e.g. your major, your expertise, your interests, etc) and write a test using GTest for your finction in [tests/q5_student_test.cc](tests/q5_student_test.cc).
We will run your code and see your printout!

Please create your test cases and run the following command to verify the functionality of your program.
```
bazel test tests:q5_student_test
```

## Question 6 (25 Points. Medium)

 Write a function ```std::vector<int> CPPLib::Flatten2DVector(const std::vector<std::vector<int>> &input)``` in [cpplib.cc](src/lib/cpplib.cc) to flatten a 2D vector into a 1D vector.

Example:\
Input: inputs = [[1, 2, 3, 4], [5, 6], [7, 8]].\
Output: result = [1, 2, 3, 4, 5, 6, 7, 8].

Write several tests using GTest for your function in [tests/q6_student_test.cc](tests/q6_student_test.cc).\
(Hint: inculde cases with empty vectors)

Please create your test cases and run the following command to verify the functionality of your program.
```
bazel test tests:q6_student_test
```

## Question 7 (30 Points. Medium)

Write a function ```double CPPLib::CalFactorial(int N)``` in [cpplib.cc](src/lib/cpplib.cc) using recursion to find the factorial of any number. Your function should accept positive numbers and return the factorial value. Further, write several tests using GTest for your function in [tests/q7_student_test.cc](tests/q7_student_test.cc) and compute the time complexity of your implementation.

*Definition of the factorial function*\
In mathematics, the factorial of a positive integer n, denoted by n!, is the product of all positive integers less than or equal to n:

```
n ! = n x (n - 1) x (n - 2) x (n - 3) ... (3) x (2) x (1)
```

For example, 4! = 4 × 3 × 2 × 1 = 24.\
The value of 0! is 1. For negative input, please return -1.

Please create your test cases and run the following command to verify the functionality of your program.
```
bazel test tests:q7_student_test
```

For question 5, 6, 7, if you want to run all the tests at the same time , you could run
```
bazel test tests:tests
```

Answer:

