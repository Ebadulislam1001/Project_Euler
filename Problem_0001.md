# Problem 1 - Multiples of 3 or 5

```
If we list all the natural numbers below 10 that are multiples of 3 or 5, we get [3, 5, 6, 9].
The sum of these multiples (3 + 5 + 6 + 9) is 23.
Find the sum of all the multiples of 3 or 5 below 1000.
```

## Approach
First of all it reminds me of the "FizzBuzz" game. The solution is also going to be a simple one.

- Just initialise a variable `sum = 0`.
- Loop over each number in the range `[1, 1000)`.
- If the number is either a multiple of `3` or `5`, add it to the `sum`.
- Declare the final value of the `sum` as the answer.

## Code
```
# Python
sum = 0
upperBound = 1000
for i in range(1, upperBound):
    if(i % 3 == 0 or i % 5 == 0):
        sum += i
print(f"Answer = {sum}")
```

## Answer
```
Answer = 233168
```

## Bonus
But why stop here!!!

If we change the value of the `upperbound` to different `powers of 10`, we see a cool pattern.
```
upperbound = 1          Answer = 0
upperbound = 10         Answer = 23
upperbound = 100        Answer = 2318
upperbound = 1000       Answer = 233168
upperbound = 10000      Answer = 23331668
upperbound = 100000     Answer = 2333316668
```
Does anyone know why?
