FENCRYPT?=./fencrypt

PREFIX=.fenc-meta.

TEXT_FILES=macbeth.txt aeschylus.txt
BINARY_FILES=ecb.jpg

all: encrypt search

encrypt: $(addprefix $(PREFIX),$(TEXT_FILES) $(BINARY_FILES))

$(PREFIX)%: %
	echo -n $* | $(FENCRYPT) -e -j $*

search:
	@echo
	-echo -n wrongpassword | $(FENCRYPT) -s crickets
	@echo
	echo -n macbeth.txt | $(FENCRYPT) -s haha
	@echo
	echo -n macbeth.txt | $(FENCRYPT) -s crickets
	@echo
	echo -n macbeth.txt | $(FENCRYPT) -s cric*
	@echo
	echo -n aeschylus.txt | $(FENCRYPT) -s άδραστου
	@echo
	echo -n aeschylus.txt | $(FENCRYPT) -s άδρασ*

clean:
	-rm *.txt* .*.txt
	-rm *.jpg* .*.jpg

macbeth.txt:
	# https://www.gutenberg.org/ebooks/2264
	curl -s https://www.gutenberg.org/cache/epub/2264/pg2264.txt | tee $@.plain > $@

aeschylus.txt:
	# https://www.gutenberg.org/ebooks/17996
	curl -s https://www.gutenberg.org/files/17996/17996-0.txt | tee $@.plain > $@

ecb.jpg:
	# https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation
	curl -s https://upload.wikimedia.org/wikipedia/commons/f/f0/Tux_ecb.jpg | tee $@.plain > $@
