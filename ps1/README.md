# Problem Set 1
## Getting oriented

All of the coding problem sets in the course should work like this:

- You will write a standalone program that reads from standard input,
  and writes to standard output. Your program will be submitted to
  Gradescope, which will automatically grade it.

- You can resubmit as many times as you want, up through the
  submission deadline.

- The standard input (stdin) will be a JSON object, where the keys are
  strings, "problem1", "problem2", ... "problem<n>".  The values will
  vary, depending on the problem.

- You will write a single JSON object to standard output (stdout),
  that have keys that are the indentical strings.  The output type
  will be specified in the problem set.

- The grading program will read your JSON, and then compare it to
  expected results.

- Your program's standard error (stderr) will be ignored. Do NOT leave
  debugging in if it writes to standard output.

- You can use any programming language you like, and incorporate any
  third-party crypto libraries you want. You will need to learn how to
  get Gradescope to incorporate your dependencies, though.
  Gradescope's testing environment is a Ubuntu-20.04-based Docker
  container, with Python3, Go, Java, C, C++ and Rust pre-installed.

- When uploading your answer to gradescope, make sure that your
  submission builds if necessary, and produces an executable file
  named "ps1".  If you use a scripting language like Python, do NOT
  use the file extension, but add a "magic" `#!` Unix comment as the
  first line of your program, e.g.:

`#!/usr/bin/env python3`


## Cheating Policy

*You must write all the code you submit.* Submitting code written by
anyone else is cheating.

I even would discourage you from even discussing the assignments with
other students, as it's often a fine line.

Instead, come to the TAs, or to me. We are here to help you. Your goal
should be to learn the material, and learn to program. If you're
learning, you'll do well enough; it's not worth the consequences of
getting cought.

And, I have cought a LOT of cheaters in my time teaching.  For
example, I've done all of the following in previous semesters, to
great success:

1) Looked for people posting parts (or all) of my assignments to common
coding Q+A sites.

2) Run cheating analytics algorithms.

3) Signed up for site where you pay people to do coding homework for
you. I find it highly satisfying for students to pay me to catch them
cheating!

For common operations like "open a file", "parse a JSON string", or
"call a library function", it's ok to copy two or three lines of code
from documentation, Stack Overflow, etc. But copying more than two or
three lines of code is probably not ok. If you do, you must clearly
cite your source in an inline comment that begins with COPIED. Citing
your source doesn't automatically make copying ok, but failing to cite
your source turns one violation into two violations. Please don't
explore the gray area of what counts as a "line of code".

## Getting started with GradeScope

GradeScope has decent documentation. However, one of the professors
from last semester's Class, Jack O'Connor, did a good introductory
video on GradeScope, that is worth a watch, even though, it's
important to node, *our problem set is different than theirs* (and all
our problem sets will be different).

[Jack's video](http://www.youtube.com/watch?v=b0gGlcHvfY0)

## The Problems

### Problem 1

In Problem 1, our goal is to simply figure out how to use JSON to read
inputs and write outputs.  The input is a list of strings, each of
which you must transform by converting all the lowercase letters to
upper case.  If you're using Python, this is easy to do, by calling
the 'upper' method on a string.  For instance:

`>>> s = "af0b21f"
>>> print(s.upper())
AF0B21F
>>>`

The input JSON for this would look like:

`{"problem 1": ["af0b21f", "deadbeeffeedface"]}`

And your output JSON for this would look like:
`{"problem 1": ["AF0B21F", "DEADBEEFFEEDFACE"]}`

You can assume throughout this assignment that hex used as input is
well formed.

I will not use spaces when I give you hex strings, and you should not
output spaces either.

### Problem 2

One issue with JSON is that its strings are UTF-8 encoded, but we
really want to be able to work with binary data, which is NOT
supported (it would be good for you to figure out the difference
outside of class if you do not understand this).  That's why we want
to be able to use hex (another common alternative that we won't use is
Base64 encoding).

First, we're going to make sure we know how to convert hex digits into
binary bytes.  I will provide you strings of hex digits, and you will
convert them, byte-by-byte, into ASCII.

Note that, for this problem, I will NOT give you any values that would
be interpreted as high ASCII.

For example, if the input is simply `{ "problem 2" : ["68656c6c65f"]
}` you should output JSON like this: `{ "problem 2" : ["hello"] }`

You need to be able to handle upper and lower case hex digits.

### Problem 3

Now, you're going to show that you can round trip items from hex, to
binary, and back to hex.  I will give you as inputs a hex string,
which you will convert to an array of bytes.  Then, add 0x20 to the
byte, PLUS the byte's offset from zero.  Then, convert the result back
to hex.

For instance, my input might be: `{"problem 3" : ["48454C4C4F"]}`

You would first convert this to an array of bytes: `[0x48, 0x45, 0x4c, 0x4c, 0x4f]`.

Yes, if you were to treat that array of bytes as a UTF-8 encoded
string, it would print "hello".  But work on it as an array of bytes
instead.

Now, add 0x20 (32) to each byte: `[0x68, 0x65, 0x6c, 0x6c, 0x6f]`

If you treat this as a UTF-8 encoded string, it would now read "HELLO".

Now, add 0x00 to the first byte, 0x01 to the second, 0x02 to the 3rd,
0x04 to the fourth, and 0x05 to the fifth.  You'd now have: `[0x68,
0x66, 0x6e, 0x6f, 0x73]`

Do all these additions modulo 256.

Now, convert this back to a hex string and output it as JSON:

`{"problem 3": ["68666E6F73"]}`


### Problem 4

For this problem, the input will be a list of positive 64-bit
integers. You will output a list of 64-bit integers, where each is
randomly selected, but LESS than the corresponding integer
provided. That is, for each list item, I will give you a value N, and
you are to output rand() modulo N.  Here, there will be automatic
testing, but we will also manually inspect your code to ensure that
you use a cryptographically strong source of randomness.


###