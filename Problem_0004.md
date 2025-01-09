# Problem 4 - Largest Palindrome Product
```
A palindromic number reads the same both ways.
The largest palindrome made from the product of two 2-digit numbers is 9009 = 99 * 91.
Find the largest palindrome made from the product of two 3-digit numbers.
```

## Intuition
We can try two things here -
- check for each pairs of 3-digit numbers, if their product is a palindrome or not.
- check for each 5-digit and 6-digit palindrome number, if it can be written as a product of two 3-digit numbers. Because the product of two 3-digit numbers has either 5 or 6 digits. 

## Approach 1
Check for all 3-digit numbers, if their product is palindrome or not.
- maintain a variable named `LPP` _(Largest Palindrome Product)_.
- for each `x` : `x` is a 3-digit number:
- for each `y` : `y` is a 3-digit and `x <= y` (to skip reflection pairs):
- if `(x * y)` is a palindrome : update LPP.

### Code 
```Python
# Python

def is_pal(num):
    return str(num) == str(num)[::-1]

LPP = 0
for x in range(100, 1000):
    for y in range(x, 1000):    # to skip reflection pairs
        product = x * y
        if (is_pal(product) and product > LPP):
            LPP = product
print(f"Answer = {LPP}")
```
The code looks fine, works fine. But wait!! I have one more trick up my sleeve.

## Approach 2
Check for all 5-digit and 6-digit palindrome number, if it can be written as a product of two 3-digit numbers or not.

Instead of going through the list of all 5-digit and 6-digit numbers, we are going to generate the palindromes only.
- All 5-digit palindromes are of the form `ABCBA`, where `A != 0`. That leaves us with only 900 combinations.
- All 6-digit palindromes are of the form `ABCCBA`, where `A != 0`. That leaves us with only 900 combinations.
- so we have a total `1800` distinct palindromes to consider.

Now the task remains to check if these palindromes can be written as a product of two 3-digit numbers or not.

We know that factors of an integer `N` exist in pairs, let `a` <= `b` be one such pair, then `a` <= `sqrt(N)` <= `b`.

Since we want both the factors to be 3-digit numbers, we can just run a loop for the `a` in range `[1000, sqrt(N)]` and check if `a` is a factor of `N` and if `b` is also a 3-digit number.

In addition, since we just want the _Largest Palindrome Product_, we can do our search in decreasing order and break out as soon as we get a match.

### Code
```Python
# Python
import math
import time

start = time.perf_counter()

def is_product(num):
    for f in range(100, int(math.sqrt(num) + 1)):
        if ((num % f) == 0 and (num / f) <= 999):
            return True
    return False

LPP = 0
ans_found = False
A = 9
while (A >= 1 and not ans_found):
    B = 9
    while (B >= 0 and not ans_found):
        C = 9
        while (C >= 0 and not ans_found):
            pal_6 = int(str(A) + str(B) + str(C) + str(C) + str(B) + str(A))
            if (is_product(pal_6)):
                LPP = pal_6
                ans_found = True
            C -= 1
        B -= 1
    A -= 1
A = 9
while (A >= 1 and not ans_found):
    B = 9
    while (B >= 0 and not ans_found):
        C = 9
        while (C >= 0 and not ans_found):
            pal_5 = int(str(A) + str(B) + str(C) + str(B) + str(A))
            if (is_product(pal_5)):
                LPP = pal_5
                ans_found = True
            C -= 1
        B -= 1
    A -= 1
if(ans_found):
    print(f"Answer = {LPP}")
else:        
    print(f"No such number exists")
```
Compared to the last code which takes `200ms`, this one takes only `30ms` on my machine.

## Answer
```
Answer = 906609 
```