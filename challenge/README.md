Challeng #1

The following python program is supposed to count the number of characters (character frequency) in a string.

```
Sample String : google.com'
Expected Result : {'o': 3, 'g': 2, '.': 1, 'e': 1, 'l': 1, 'm': 1, 'c': 1}
```

```
def count_chars(phrase):
    counts = {}
    for letter in phrase:
        counts[letter] = counts.get(letter, 0) + 1
    return counts
```

Write a set of unit tests to make sure that it functions properly



# Challenge #2

Implement a function that takes as input three variables, and returns the largest of the three. Do this without using the Python max() function!

The goal of this exercise is to think about some internals that Python normally takes care of for us. All you need is some variables and if statements!

__Then...__

Write a set of unit tests to make sure that it functions properly


# Challenge 3:

The followng python program computes the collatz series for any given integer value < 100.

For instance, starting with n = 12, one gets the sequence 12, 6, 3, 10, 5, 16, 8, 4, 2, 1.


Read about it here: https://en.wikipedia.org/wiki/Collatz_conjecture 


```
# code goes here
# The conjecture is that no matter what value of n, the sequence will always reach 1.
def collatz(x):
    if x == 1:
        return x + 1
    elif x == 2:
    	  return 2
    elif x%2 ==0:
        return collatz(x/2)
    else:
        return collatz(x*3 + 1)
```

Write a set of unit tests to check if it functions properly

If it does not, change it to make sure it function properly
