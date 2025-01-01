# Problem 1 - Multiples of 3 or 5
```
If we list all the natural numbers below 10 that are multiples of 3 or 5, we get [3, 5, 6, 9].
The sum of these multiples (3 + 5 + 6 + 9) is 23.
Find the sum of all the multiples of 3 or 5 below 1000.
```

## Approach 1
First of all it reminds me of the "FizzBuzz" game. The solution is also going to be a simple one.
- Just initialise a variable `sum = 0`.
- Loop over each integer in the range `[1, 1000)`.
- If the number is a multiple of `3` or `5`, add it to the `sum`.
- Declare the final value of the `sum` as the answer.

Time Complexity = `O(N)`, here N = 1000

### Code
```Python
# Python
N = 1000

sum = 0
for i in range(1, N):
    if(i % 3 == 0 or i % 5 == 0):
        sum += i
print(f"Answer = {sum}")
```

## Approach 2
But instead of running a loop for each number in the range `[1, 1000)`, we can calculate the required sum directly by using the following formula:
```
sum of all multiple of 3 or 5
    = sum of all multiple of 3
    + sum of all multiple of 5
    - sum of all multiple of both 3 and 5
```
here ***all multiples*** means ***all multiples in the given range***.

Adding all the multiples of 3 and then the multiples of 5 will cause the numbers that are multiples of both 3 and 5 to get added twice. That's why we have to subtract those numbers in the end so that they get added only once. Also we can call the numbers that are multiples of both 3 and 5 simply as the numbers that are multiples of 15, since LCM(3, 5) = 15.

Since the numbers that are multiple of 3 (or 5 or 15) form a finite A.P., we can easily calculate their sum using the formula of finding the sum of a finite A.P.
```
sum of a finite A.P. = (count of terms) * (middle term)
```
Time Complexity = `O(1)`

### Code
```Python
# Python
N = 1000

def sum_of_multiples(N, factor):
    count_of_terms_in_AP = (N - 1) // factor
    middle_term_in_AP = factor * (count_of_terms_in_AP + 1) / 2
    sum_of_terms_in_AP = count_of_terms_in_AP * middle_term_in_AP
    return int(sum_of_terms_in_AP)

sum = sum_of_multiples(N, 3) + sum_of_multiples(N, 5) - sum_of_multiples(N, 15)
print(f"Answer = {sum}")
```

## Answer
```
Answer = 233168
```

## Bonus
But why stop here!!!

If we set the value of the `N` to different `powers of 10`, we get to see a cool pattern.
```
N = 10         Answer = 23
N = 100        Answer = 2318
N = 1000       Answer = 233168
N = 10000      Answer = 23331668
N = 100000     Answer = 2333316668
```
Does anyone know why?
