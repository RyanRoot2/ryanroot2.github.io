# Hash Algorithms

## Introduction

### What is a hash function?
A hash function, or hash algorithm, is a function that converts an input into a string of bytes, which is often expressed using hexidecimal.
The result is pseudo-random (seemingly random) and is typically referred to as the hash value.

Hash functions are commonly used for purposes such as data integrity verification (making sure nothing has changed), storing passwords, and digital signatures.

It's important to note that hash functions are one-way, it's impossible to get the input back from the output.

Hash functions have three main properties:

* Deterministic - the same input always gives the same hash value
* Efficient - they are fast to compute
* Avalanche Effect - a small change to the input produces a significantly different output

### Use case: storing a password
When a user registers for an account, they create a password. Instead of storing that password, the application will use a hash function to
generate a hash value of the password which is stored instead.

When a user tries to log in, whatever password they enter will be input into the same hash function and the resultant hash value can be compared to
the one stored in the database.

Because of determinism, we can say that if the hash values are the same, the password has been entered correctly.

### An example of a (bad) hash function
Suppose I create an account using the following password: **P7v8kX2a** <br>
One way to create a hash value of this is to take the ASCII values for each character and add them up.

Here is how this can be done in Python:

```py
# Define the password
password = "P7v8kX2a"

# Generate the ASCII values for each character in the password
ascii_values = [ord(char) for char in password]

# Calculate the sum of the ASCII values
ascii_sum = sum(ascii_values)

# Output the ASCII values and the sum
ascii_values, ascii_sum
```

This will return the following values:
```py
ASCII values: [80, 55, 118, 56, 107, 88, 50, 97]
ASCII sum: 651
```

In this case, the value stored in the database would be **651** instead of the password.

There are a few reasons this is a bad hash function:

1. **Not Unique**
    Many combinations of numbers add up to 651 - that means somebody could enter an incorrect password
    and be granted access to the account. Likewise "ABC" and "CBA" would have the same hash value.
    Another way of saying this would be to say that the set of possible sums is smaller than the set of possible passwords. *6 = 5+1*, *6 = 4+2*, *6 = 3+3*, etc.
2. **Deterministic and Predictable**
    Given a hash value, an attacker could easily reverse-engineer possible combinations of characters that result in that sum. This makes the function vulnerable to brute force attacks.
3. **No Avalanche Effect**
    A change to the input does not provide a *significant* change to the output. In fact, changing the letter "A" to the letter "B" in the input would
    simply increase the ASCII sum by 1.
4. **Brute Force Vulnerability**
    Summing ASCII values is extremely fast and trivial to compute. This allows attackers to generate and compare possible sums almost instantly, drastically reducing the time needed for a brute-force attack. Moreover, the hash value itself can start to reveal information about the password. At the most trivial level, if the ASCII sum is greater than *1* then the password can't simply be 'A'. If the ASCII sum is greater than *127* (the maximum ASCII value), the password must be at least two characters in length.

