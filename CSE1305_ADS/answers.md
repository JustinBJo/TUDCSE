# Answers to Weblab Questions

---

# Week 1
## 1
1. T
2. F
3. T
4. F

## 2
line 1: c0 = 1 (calling the method)<br>
line 2: c1 = 2 (initialisation, getting the length of arr) <br>
line 3: c2 = 1 (initialisation)<br>
line 4: c3 + c4 * n = 1 + (n+1) + 2n (initialisation, comparing, incrementing)<br>
line 5: c5 * n = 2n (getting arr[j] and multiplication, but it is done n times)<br>
line 7: c6 = 1  (return)

T(n) = c0 + c1 + c2 + c3 + c4 + n * c5 + n * c6 <br>
     = (c4 + c5) * n + c0 + c1 + c2 + c3 + c6<br>
     = 3n + 7  
     = O(n)

## 3
f1:<br>
line 1: c0 <br>
line 2: c1<br>
line 3: c2<br>
line 5: c3 + c4 * n<br>
line 6: c5 * n<br>
line 8: c6<br>

T(n) = (c0 + c1 + c2 + c3 + c6 + (c4 + c5) * n)
     = ca + cb * n

The method is called n times, each time n = n - 1.

T(n) = c * (n + n-1 + ... + 1)<br>
     = c * n(n+1)/2<br>
     = O(n^2)


f2:<br>
line 1: c0<br>
line 2: c1<br>
line 3: c2<br>
line 6: c3<br>
line 8: c4<br>

The method is called n times.

T(n) = (c0 + c1 + c2 + c3 + c4) * n<br>
     = O(n)

## 4
1. 2^15, 2log2n, 2n+100log2n, 6n, 2nlog2n, 4nlog2n+2n, n^2+5n, 100n^3, 2^n
   - 2^n -> O(2^n)
   - 100n^3 -> O(n^3)
   - 2^log2n -> O(n)
   - 2n + 100log2n -> O(n)
   - 4nlog2n + 2n -> O(nlogn)
   - n^2 + 5n -> O(n^2)
   - 6n -> O(n)
   - 2^15 -> O(1)
   - 2nlog2n -> O(nlogn)
2. 1, 2

## 5

## 6
1. 2
   - T(1) cannot call T(n)
   - correct
   - not a recurrence relationship
   - T(1) does not have n
   - not a recurrence relationship
2. 3, 5
   - not a valid recurrence equation
   - not a closed form
   - correct
   - not a closed form
   - correct
3. 4
   - not necessarily, because T(n) is in terms of T(n-5) which means it is number of times it was called / 5.
   - incorrect
   - it is the length of the input array.

## 7
1. T(n) = T(n-2) + c, T(-2) = T(-1) = b
   - b is the set of constant operations that account for the bases cases (line 3, 5, 7)
   - c accounts for the guards of the if statements and the additions needed for the recursive call.
   - T is the function that represents the recursive function
   - The base cases are T(-2) and T(-1) to account for both the odd and even cases respectively.
   - Each recursive call n decreases by 2 because we increment low and decrement high.
2. .
   - a) b + cn/2 + c
     - T(n) = T(n-2) + c
     - T(n) = (T(n-4) + c) + c
     - T(n) = T(n-2k) + kc
     - take k = n/2 + 1
     - T(n) = T(-2) + cn/2 + c
     - T(n) = b + cn/2 + c
   - b) Proof by Induction
     - Base case:
       - At n = -2, T(-2) = b + (c * -2) / 2 + c = b
       - This correctly corresponds to the base case of the code
     - Inductive Hypothesis:
       - Suppose that the closed form of T(n-2) is correct: T(n-2) = c * (n-2)/2 + c + b
     - Inductive case: prove that the recursive case T(n) = T(n-2) + c correctly corresponds to the closed-form solution.
       - T(n) = T(n-2) + c
       - = (c * (n-2)/2 + c + b) + c (IH)
       - = ((n-2)/2 + 1) * c + c + b
       - = (n/2) * c + c + b
     - This correctly yields the closed form. By induction, it is now proven that T(n) = c * n/2 + c + b is correct for every integer n >= -2
3. O(n)
   - T(n) = n*d + e where d = c/2 and e = c+d.
   - The constant term can be removed because as n grows larger this constant will be insignificant.
   - The coefficient d can also be removed because with or without this factor the function will still have linear growth rate.
   - This leaves us with T(n) = n, which is a linear growth.
   - Therefore, the time complexity is O(n).
4. Proof
   - Show that there exists a real c' > 0 and an integer n0 >= 1 such that b + cn/2 + c <= c'n for all n >= n0.
   - Take c' = 1 + b + c and n0 = 2
   - Prove that b + cn/2 + c <= n + bn + cn for all n >= 2
   - n - cn/2 -c + cn + bn - b = n + (n/2 - 1)c + (n - 1)b >= 0 for all n >= 2
   - We know that c and b are all positive, so we can tell that all terms are positive (or zero)
   - The equation holds.

## 8
1. True
2. False
   - If the array is never used it can be less than n.
3. False

## 9
1. False
2. False
3. False
4. True
5. False
6. True
7. True
8. True
9. False
10. True

## 10
1. False
2. 5
3. 3
4. 6

## 11
1. Linear recursion
2. Binary recursion

Types of recursive functions:
- Linear recursive functions
  - functions that only make a single call to itself each time the function runs
- Binary recursive functions
  - functions that call itself twice in each run
- Multiple recursive functions
  - more than twice


# Week 2
## 1
1. T
2. F
3. T
4. T
5. F
6. F
7. T

## 2
1. addFirst
2. DLL

## 3
3
- We don't have to manually set to null because there is no prev pointer and the garbage collector will remove the implicit head.

## 4
1. addFirst
2. removeLast
3. addFirst
4. removeFirst

## 5
1. dequeue
2. Queue
3. Array

## 6
1. T(n) = c0 + c1n + c2(n+1) = c3 + c4 * n
   - c3 = c0 + c2
   - c4 = c1 + c2
   - n is the size of the stack s
   - c0 represents the constant-time operations on line 2, 3, 4[1], 8, 9, 10[1], 14
   - c1 represents the constant-time operations on line 4[3], 5, 10[3], 11
   - c2 represents the constant-time operations on line 4[2] and 10[2]
2. O(n)
   - constant term c3 can be discarded because as n grows larger, the constant term has little impact on the growth rate of the function
   - coefficient c4 can also be discarded because with or without c4 the function has linear growth rate
   - therefore we are left with T(n) = n, which has O(n) complexity.

## 7
1. T(n) = c0 + c1n + c2(n+1) = c3 + c4 * n
   - c3 = c0 + c2
   - c4 = c1 + c2
   - n is the size of the queue q
   - c0 represents the constant-time operations on line 2, 3, 4, 5[1], 15, 16[1], 20
   - c1 represents the constant-time operations on line 5[3], 6, 10, 11, 16[1], 17
   - c2 represents the constant-time operations on line 5[2] and 16[2]
2. O(n)
    - constant term c3 can be discarded because as n grows larger, the constant term has little impact on the growth rate of the function
    - coefficient c4 can also be discarded because with or without c4 the function has linear growth rate
    - therefore we are left with T(n) = n, which h


# Week 3
## 1
1. each node in the list
2. the references
3. no