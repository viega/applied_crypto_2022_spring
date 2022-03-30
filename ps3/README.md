# Problem Set 3: Understanding the RSA Math
In this assignment, you're going to encrypt small numbers... nothing big enough to be secure. Nor will you be doing any padding, etc.

You can assume that any computations you have to do as part of the testing will fit into the machine's standard floating point size (In many languages, the data type 'double', short for 'double float').

## Due Date
The assignment is due on April 13th, at 5pm Eastern time. Anyone who needs an extension can have a single one week extension without asking us, but no further extensions will be given.

A sample input and associated output file is provided in this directory.

Submit an executable names ps3, taking input and output in the same way as with the other programming assignments (ps1 and ps2).

## Cheating Policy

As with all assignments in this class, *You must write all the code
you submit.* Submitting code written by anyone else is cheating.

I even would discourage you from even discussing the assignments with
other students, as it's often a fine line.

Instead, come to the TAs, or to me. We are here to help you. Your goal
should be to learn the material, and learn to program. If you're
learning, you'll do well enough; it's not worth the consequences of
getting cought.

## The Problems
We're going to build up to to full encryption by implementing the pieces.  In all cases, the JSON inputs will be positive integers.

### Problem 1

For RSA, in real-world scenarios, we need to select two incredibly large random numbers. One way we can do this is by picking a random number, and then testing it for primality. In this exercise, we'll supply you with an array of integers that are all positive, and representable in 32 bits. For each integer, you will output a boolean value of `true` if it is prime, and `false` if it is not.

You're welcome to use a fancy probablistic algorithm, such as the Miller-Rabin test (which is very commonly used in crypto libraries), but you should be able to use trial division... even though it might take a while to grade (2^32 is a lot of trials... at least skip even numbers after 2).

Note that if we were giving you 64-bit values, your run time on a real prime would be way too long to be practical, never mind a 4096-bit prime.

Input:
- *nums*: An array of integers to test for primality.

### Problem 2

Now that we know how to test for primality, you could validate choices for `p` and `q`. But what you're really going to do is use it to, given values for `p` and `q` that are prime, find the lowest possible value of `e`.

Remember that `e` needs to be relatively prime to the least common multiple of `p-1` and `q-1`.  That means, you need to find the least common multiple-- the smallest integer into which `p-1` and `q-1` both evenly divide.

Inputs:
- *p*: A prime number
- *q*: A second prime number

You output an integer, the lowest possible value of `e`.

### Problem 3

Now we need to be able to compute d, by finding the modular inverse of e. Remember that the number we're looking for, when multiplied by e and reduced by[^1] LCM(p-1, q-1), will give the value 1.

Inputs:
- *p*: A prime number
- *q*: A second prime number

You output an integer, the value of `d` such that `d` is the modular inverse of the lowest possible value of `e` (re-use what you did in step 2 to get `e`).

### Problem 4

Great, we're ready to encrypt. Raw encryption and decryption in RSA consist of a single exponentiation operation in our multiplicative group, so we've already done all the hard work.

Here, you'll be given a public key (`e` and `n` together comprise the public key), and a plaintext `x`.  You'll return the ciphertext.

Inputs:
- *e*: The exponent to which we're going to raise `x`.
- *n*: The modulus we reduce by.
- *x*: An integer representing a value we're going to raise to some power.

You output the ciphertext.

### Problem 5
Okay, now let's decrypt!  We will give you the values of `p` and `q` to use.  You will again select the smallest valid value of `e`. That way we'll already have your 'public' key.  We'll also send you an encrypted number, `y`.

From this information, compute `n` and your private key (`d`), and operate on `y`, returning the decrypted number.

Inputs:
- *p*: A prime number
- *q*: A second prime number
- *y*: A number to decrypt

You output the plaintext.

--


[^1]: 'Reduced by' means use the modulus operator.