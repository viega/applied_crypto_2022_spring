# Project Examples Folder

This folder contains a couple of example files which were encrypted with the
`fencrypt` program as described in the project.

All the original plaintext files are also saved with `.plain` suffix for
reference. Files are encrypted with the password being the filename itself.

See `Makefile` for all shell commands which were used to:

- download files
- encrypt files
- search for some terms in the encrypted files

Note that while encrypting files `-j` flag was used which shows actual master
key which was used to encrypt all of the files.

```bash
➜ make clean all

# https://www.gutenberg.org/ebooks/2264
curl -s https://www.gutenberg.org/cache/epub/2264/pg2264.txt | tee macbeth.txt.plain > macbeth.txt
encryptiing with password: 'macbeth.txt'
echo -n macbeth.txt | ./fencrypt -e -j macbeth.txt
{
    "macbeth.txt": "44770de6f1857b85de1c40566aae98385413eef184daff187b7931fde6417dc0"
}

# https://www.gutenberg.org/ebooks/17996
curl -s https://www.gutenberg.org/files/17996/17996-0.txt | tee aeschylus.txt.plain > aeschylus.txt
encryptiing with password: 'aeschylus.txt'
echo -n aeschylus.txt | ./fencrypt -e -j aeschylus.txt
{
    "aeschylus.txt": "835b9d7898e4c6900f27630f2a4bd6cd997de70a135f0a2071511c8a5f20cea5"
}

# https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation
curl -s https://upload.wikimedia.org/wikipedia/commons/f/f0/Tux_ecb.jpg | tee ecb.jpg.plain > ecb.jpg
encryptiing with password: 'ecb.jpg'
echo -n ecb.jpg | ./fencrypt -e -j ecb.jpg
{
    "ecb.jpg": "fee9c70ff632e4766cf5511f1abdca22db930726f2cad59c7c3016e504e558a4"
}

echo -n wrongpassword | ./fencrypt -s crickets
aeschylus.txt: password does not match
ecb.jpg: password does not match
macbeth.txt: password does not match
no files to search with matching password
make: [Makefile:20: search] Error 1 (ignored)

echo -n macbeth.txt | ./fencrypt -s haha
aeschylus.txt: password does not match
ecb.jpg: password does not match
['haha'] were not found in any of the files

echo -n macbeth.txt | ./fencrypt -s crickets
aeschylus.txt: password does not match
ecb.jpg: password does not match
macbeth.txt

echo -n macbeth.txt | ./fencrypt -s cric*
aeschylus.txt: password does not match
ecb.jpg: password does not match
macbeth.txt

echo -n aeschylus.txt | ./fencrypt -s άδραστου
ecb.jpg: password does not match
macbeth.txt: password does not match
aeschylus.txt

echo -n aeschylus.txt | ./fencrypt -s άδρασ*
ecb.jpg: password does not match
macbeth.txt: password does not match
aeschylus.txt
```
