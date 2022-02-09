# Problem Set 2: Attacking Bad Crypto, block modes edition
## Due Date

This assignment is due on Feb 23rd, at 5pm Eastern time.  Late
assignments will be accepted for one week.

A sample input file and associated output file is provided in this directory.

Submit with an executable named ps2, taking input and output in the
same way as the last assignment.

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

In the following problems, all inputs will be hex-encoded binary,
unless otherwise noted.

Your outputs will all be hex-encoded binary.

In all cases in this assignment, AES is the encryption algorithm we're
going to be using under the hood, but you don't need to get it working
for this assignment.  You're just going to be attacking stuff that I
encrypt with AES.

### Problem 1

We're going to attack a stock trading system that uses ECB mode.

Imagine a scenario where you are secretly recording all my ciphertext
as it leaves my machine. I left my keyboard unlocked one day, and you
managed to see my entire history of trades, which includes plenty of
buying and selling of the same stocks.  You can match that to the
ciphertexts.


We talk at the water cooler a lot. You know I have a LOT of shares in
Apple now, and that I think Microsoft is about to crash.  But you
secretly want me to fail, so you're going to replace every order I
make trying to sell my Microsoft shares with an order to sell Apple
shares instead, using old ciphertexts.

The format of messages in the system is as follows:

- When unencoded, all messages will be strings of 16 byte ASCII commands.
- A command's first byte is either B or S (for buy or sell).
- The second byte is always a space
- The third, fourth, fifth and sixth byte are a stock ticker symbol, eg, AAPL
- The seventh byte is a colon
- The eighth byte is a space
- The rest of the bytes are a representation of how many shares in the order, padded by spaces on the right.

For instance, the contents of the following string would be two different orders:
"S AAPL: 1000    S MSFT: 1000    "

In this system, each distinct trade should always encrypt to the same
value, when the same key is used.

For the problem, I will pass you the following inputs:

- *old_pt:* A sequence of old trades that I've made, hex encoded.
- *old_ct:* The ciphertext associated with those old trades, hex encoded.
- *op_1:*  An ASCII value (NOT hex encoded) that will be either B or S
- *co_1:* The ASCII value (NOT hex encoded) of a stock ticker.
- *op_2:* An ASCII value (NOT hex encoded) that will be either B or S.
- *co_2:* The ASCII value (NOT hex encoded) of a second stock ticker.
- *new_trades:* A LIST of ciphertexts corresponding to hex-encoded trades, representing my trades across a number of days.

Your goal will be as follows:

To output a NEW list of hex-encoded trades, where all the trades of
type op_1 by company_1 (so far as you can see them) are replaced by
the biggest trade you've previously seen of type op_2 for company_2.

### Problem 2
I didn't catch you, but I'm still employed. The powers that be
realized that ECB mode was a bad idea, and they've "upgraded" to CTR
mode.  However, they didn't realize that CTR mode needs a unique
nonce, so every series of trades is encrypted with the same keystream.

That means, if you have an old plaintext / ciphertext pair, you can
read any messages encrypted with the same key/nonce combo, without
having to know either the key or the nonce!

One day I tell you I'm about to make the trade of a lifetime, but I
won't tell you the secret.  I want to, but I'm bound by
confidentiality, and I'm too much of a rule follower to tell you, even
though I really want to.  But, since I won't share my hot tip, you're going
to decrypt today's trade, and learn it anyway!


For the problem, I will pass you the following inputs:

- *old_pt:* A series of old trades you know about, in plaintext (hex encoded).
- *old_ct:* The ciphertext that was associated with those trades.
- *new_ct:* A single ciphertext for you to decrypt, which will be no longer than the old ciphertext.


You will output the trades that I made today, as a hex-encoded string.

### Problem 3

Somebody realized their mistake, and our trading system now uses
unique nonces every day.  So having today's plaintext / ciphertext
doesn't help you read my trades tomorrow.

Still, you really would like to get me fired ASAP.  So you think back
to that time you learned about one-time-pads, and how easy it was to
change values, even if you didn't really know what they were.

So you decide that today, you're going to change ALL my buys to sells,
and all my sells to buys.

For this problem, I will pass you the following input:

- *todays_ct:* The ciphertext associated with today's trades.

You will output a transformed ciphertext, where you have replaced all
the buys with sells, and all the sells with buys.

### Problem 4

I got really lucky-- the market yesterday did the OPPOSITE of what I
expected, but somehow I got lucky, and managed to enter "buy" when I
thought I was selling, and vice versa.

You know that wasn't luck, and so you're more angry with me than ever.
You also are worried about getting caught, so you decide it's not such
a great idea to mess with all of my trades.  You're just going to wait
until I tell you about my next BIG trade.

And, I do tell you about it, because this one isn't a secret, I still
have no idea you hate me... I thought we were close!??

So when I tell you about my big trade, you spring into action.  You
take my next trade, and you both change it from a buy to a sell, and
change the number of shares.

You do this with every big trade I do, until I... get fired for incompetence.

For this problem, I will pass you the following inputs:

- *trade_list:*  A list of ciphertexts. It will only be a single trade per day, not a list of trades.
- *expected_num:* A list of the same size, indicating the number of shares I think I'm buying or selling on any particular day.   This will come as a proper JSON integer.
- *actual_num:*   A corresponding list containing the number of shares you're going to change my order to be.

You will output the list of transformed ciphertexts, with the new numbers, and
the changed operations.
