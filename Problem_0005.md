# Problem 5 - Smallest Multiple
```
2520 is the smallest number that can be divided by each of the numbers from 1 to 10 without any remainder.
What is the smallest positive number that is evenly divisible by all of the numbers from 1 to 20?
```

## Intuition
Smallest positive number that is evenly divisible by all numbers from 1 to 20 is basically their **LCM** _(Lowest Common Multiple)_.

## Approach
Find the `LCM` of first 20 positive integers using
```
LCM(a, b) = (a * b) / GCD(a, b)
```
where `GCD` _(Greatest Common Divisor)_ can be calculated using ***Euclid Division Algorithm***.
```
GCD(a, 0) = a
GCD(a, b) = GCD(b, a % b)
```

### Code 
```Python
# Python
N = 20

def GCD_of(a, b):
    if(a * b == 0):
        return a + b
    return GCD_of(b, a % b)

def LCM_of(a, b):
    return (a // GCD_of(a, b)) * b

multiple = 1
for num in range(1, N + 1):
    multiple = LCM_of(num, multiple)
print(f"Answer = {multiple}")
```

## Answer
```
Answer = 232792560
```