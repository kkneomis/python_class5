# Python Testing

Types of errors that can be caught:

* Syntax errors: unintentional misuses of the language
* Logical errors: when the algorithm (which can be thought of as "the way the problem is solved") is not correct. 

Unit testing, specifically tests a single "unit" of code in isolation. A unit could be an entire module, a single class or function, or almost anything in between. 


__Step 1: Create a file called primes.py with the following__


```python
def is_prime(number):
    """Return True if *number* is prime."""
    for element in range(number):
        if number % element == 0:
            return False

    return True

def print_next_prime(number):
    """Print the closest prime number larger than *number*."""
    index = number
    while True:
        index += 1
        if is_prime(index):
            print(index)
```

If we wanted to test print_next_prime, we would need to be sure that is_prime is correct, as print_next_prime makes use of it.


__Step 2: Create a file called test_primes.py__

```python
import unittest
from primes import is_prime

class PrimesTestCase(unittest.TestCase):
    """Tests for `primes.py`."""

    def test_is_five_prime(self):
        """Is five successfully determined to be prime?"""
        self.assertTrue(is_prime(5))

if __name__ == '__main__':
    unittest.main()
```

The file creates a unit test with a single test case: test_is_five_prime. Using Python's built-in unittest framework, any member function whose name begins with test in a class deriving from unittest.TestCase will be run, and its assertions checked, when unittest.main() is called.


`self.assertTrue` is rather self explanatory, it asserts that the argument passed to it evaluates to True. The `unittest.TestCase` class contains a number of assert methods, so be sure to check the list and pick the appropriate methods for your tests. Using `assertTrue` for every test should be considered an anti-pattern as it increases the cognitive burden on the reader of tests.


Each test should test a single, specific property of the code and be named accordingly. To be found by the unittest test discovery mechanism (present in Python 2.7+ and 3.2+), **test methods should be prepended by test_** (this is configurable, but the purpose is to differentiate test methods and non-test utility methods).


__Step 4: Fixing the error__

```python
def is_prime(number):
    """Return True if *number* is prime."""

    for element in range(2, number):
        if number % element == 0:
            return False

    return True

def print_next_prime(number):
    """Print the closest prime number larger than *number*."""
    index = number
    while True:
        index += 1
        if is_prime(index):
            print(index)
```

__Step 5: Add another method to the PrimesTestCase class.__

```python
def test_is_four_non_prime(self):
    """Is four correctly determined not to be prime?"""
    self.assertFalse(is_prime(4), msg='Four is not prime!')
```

Note that this time we added the optional `msg` argument to the `assert` call. If this test had failed, our message would have been printed to the console, giving additional information to whoever ran the test.


__Step 6: One edge case__

Is 0 a prime number?

Add another method to the PrimesTestCase class

```python
def test_is_zero_not_prime(self):
    """Is zero correctly determined not to be prime?"""
    self.assertFalse(is_prime(0))
```     

__Step 6: Another edge case__

The tests now pass. How will our function handle a negative number? It's important to know before writing the test what the output should be. In this case, any negative number should return False:

```python
def test_negative_number(self):
    """Is a negative number correctly determined not to be prime?"""
    for index in range(-1, -10, -1):
        self.assertFalse(is_prime(index))
```

Or...

```python
def test_negative_number(self):
    """Is a negative number correctly determined not to be prime?"""
    self.assertFalse(is_prime(-1))
    self.assertFalse(is_prime(-2))
    self.assertFalse(is_prime(-3))
    self.assertFalse(is_prime(-4))
    self.assertFalse(is_prime(-5))
    self.assertFalse(is_prime(-6))
    self.assertFalse(is_prime(-7))
    self.assertFalse(is_prime(-8))
    self.assertFalse(is_prime(-9))
```

Or... 

```python
def test_negative_number(self):
    """Is a negative number correctly determined not to be prime?"""
    for index in range(-1, -10, -1):
        self.assertFalse(is_prime(index), msg='{} should not be determined to be prime'.format(index))
```

__Step 6: Fixing code properly__

Don't do this

```python
def is_prime(number):
    """Return True if *number* is prime."""
    if number < 0:
        return False

    if number in (0, 1):
        return False

    for element in range(2, number):
        if number % element == 0:
            return False

    return True
```

Instead...do this

```python
def is_prime(number):
    """Return True if *number* is prime."""
    if number <= 1:
        return False

    for element in range(2, number):
        if number % element == 0:
            return False

    return True
```

Source: https://jeffknupp.com/blog/2013/12/09/improve-your-python-understanding-unit-testing/
