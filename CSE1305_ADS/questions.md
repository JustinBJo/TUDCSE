# Weblab Questions

---

# Week 1
## 1. Big Oh Notation
Q.
1. When considering time complexity, Big Oh notation expresses how the computation time of a method changes with respect to its input size. (T/F)
2. Time and space complexity are dependent on the hardware used. (T/F)
3. n^k is O(n^m) for all m >= k (T/F)
4. The constant factors are not important because they have no real life impact when running the program (T/F)

## 2. Code Analysis - Time Complexity I
For the code snippet below, express the time complexity in terms of a polynomial representation. Simplify your polynomial representation to derive the time complexity in Big Oh notation.

Explain your answer by counting the primitives (using constants, not numbers) per line that you used in the polynomial expression..

```
public static int product(int[] arr) {
  int n = arr.length;
  int total = 1;
  for (int j = 0; j < n; j++) { 
    total *= arr[j];
  }
  return total;
}
```

## 3. Code Analysis - Time Complexity II
The recursive functions f1 and f2 both produce the same output, i.e. f1(0,n) == f2(0,n) for a given input n.

For both f1 and f2, draw out their recursive trace on paper. Based on this trace, state and explain their runtime complexity in terms of big-Oh notation.

```
public static int f1(int tot, int n) {
  if(n == 0){
    return tot;
  }
  for(int i = 1; i <= n; i++) {
    tot += i;
  }
  return f1(tot, n-1);
}

public static int f2(int tot, int n) {
  if(n == 0) {
    return tot;
  }

  tot += n*(n+1)/2;

  return f2(tot, n-1);
}
```

## 4. Comparing time complexities of function
1. The following functions have all been analysed in terms of time complexity. Choose the correct ranking from the lowest asymptotic growth rate to the highest asymptotic growth rate.
   - 2^n 
   - 100n^3 
   - 2^log2n
   - 2n+100log2n 
   - 4nlog2n+2n 
   - n^2+5n 
   - 6n 
   - 2^15 
   - 2nlog2n
2. Select all answers that have identical asymptotical growth rates when expressed in the tightest big-Oh notation.
   - (Hint: consider when limn→∞f(n)), where f(n) is the complexity function in big-Oh notation that you derive from the expressions in the answers).
   - 3nlog2n  ,  nlog2n+n
   - 2^log2 5n  ,  100n+5log2n
   - 10^10  ,  3n
   - n4  ,  10n2+10n3


## 5. Time Complexity - Proof
Given functions f(n) = n+5  and g(n)=n show that f(n) is O(g(n)).
1. State the conditions for this to hold including the mathematical relationship that f(n) and g(n) must have.
2. Give a detailed mathematical proof that shows that the conditions hold.


## 6. Recurrence Equations
1. For the following equations, select which express a recurrence relationship.
   - T(1)=a^nT(n−5)+b
   - T(n)=a^nT(n−5)+b
   - T(n)=a+n^4 
   - T(1)=n
   - T(n)=b+a(n−1)
2. For the following equations, select which express closed form solutions of recurrence equations
   - T(1)=n
   - T(1)=anT(n−5)+b
   - T(n)=a+n4
   - T(n)=anT(n−5)+b
   - T(n)=b+a(n−1)
3. Consider the following recurrence equation: T(n)=anT(n−5)+b
   - n specifies the number of times the recursive method has been called
   - n is the upper bound of the allowed input size
   - n is an input array or data structure
   - All of the above is wrong


## 7. Manipulating Recurrence equations
For the code snippet below, work out what the worst-case computational complexity is in terms of big-Oh notation.

```
/** Return 1 if x is in arr, else 0 **/
public static int search(int[] arr, int low, int high, int x) {
  if (high < low)
    return 0;
  if (arr[low] == x)
    return 1;
  if (arr[high] == x)
    return 1;
  return search(arr, low+1, high-1, x);
}
```

For the following questions, take into account that n, the amount of elements that is still to be searched, is high - low.

1 - Derive the recurrence equation for the runtime of this code and explain all the terms.

2a - Normal version) Derive the closed-form solution of this recurrence equation, for the case where n is even.

2a - Hard version) Derive the closed-form solution of this recurrence equation (hint: you will need ⌊x⌋, which is the floor function).

2b - Optional (not part of the exam material)) Show using a proof by induction that the closed form is correct with respect to the recurrence equations you found at (1).

3 - Simplify the given closed-form equation and state the computational complexity of the search method in terms of Big Oh notation. Explain your answer, but a full proof is not needed here (you can do that as extra practice in the question below).

4 - Optional (extra practice)) Prove that the closed-form equation you found at (2) has the time complexity you found at (3).

## 8. Space Complexity
1. When considering space complexity, Big Oh notation expresses the growth rate of the space a method takes up in memory as a function of the input size. (T/F)
2. Imagine a function with input parameter of type array. Suppose this array is of size n, then this function’s space complexity can never be less than O(n). (T/F)
3. Time complexity is always more important than space complexity. (T/F)

## 9. Recursion
1. A recursive function makes only one call to itself. (T/F)
2. Recursion is unique to the Java programming language. (T/F)
3. If we have a recursive function with header int func(int x), then in each recursive call, x will be less than in the previous call. (T/F)
4. Stack overflows can be caused by recursive functions. (T/F)
5. The base case allows the function to do more recursive calls. (T/F)
6. The base case of a recursive function can contain more operations than just a single return statement. (T/F)
7. No recursive calls are made in the base case. (T/F)
8. It is possible to have more than one base case in a recursive function. (T/F)
9. A recursive call stops a function from performing any more computations or further operations on its input.
10. Calling a recursive function can lead to arrival at the base case. (T/F)

## 10. Code Analysis - Recursion I
Study the code below:

```
public static int foo(int num) { 
  if (num == 0){ 
    return 1;
  } else {   
    return num * foo(num - 1);
  } 
} 
```

1. This is an iterative function. (T/F)
2. State which line of code (if any) is making a recursive call (line numbers are provided in the pseudo code).
3. State which line of code contains the base case.
4. If the function is called with the number 5, how often will foo be on the stack.

## 11. Code Analysis - Recursion II
For the functions shown, state whether they have no recursion, binary recursion, linear recursion or multiple recursion.

foo1

```
public int foo1(int[] data, int a, int b) {
  if (data[a] < data[b]){
    return foo1(data, a, b/2);
  }
  if (data[a] > data[b]){
    return foo1(data, a+1, b);
  }
  return data[a];
}
```

foo2

```
public int foo2(int a) {
  if (a <= 1){
    return a;
  } else {
    return foo2(a - 1) + foo2(a - 2);
  }
}
```

# Week 2
## 1. Tail Recursion
For the following methods, indicate whether they are tail recursive or not.

1
```
public int f(int n) {
  if (n == 0)
    return 42;
  else
    return f(n - 1);
}
```
2
```
public int f(int n) {
  if (n == 0)
    return 1;
  else
    return n * f(n - 1);
}
```
3
```
public int f(int n, int m) {
  if (n == 0)
    return m;
  else
    return f(n - 1, m * n);
}
```
4
```
```