.PHONY: all

all: make-example

install: make-example
	install -D make-example $(DESTDIR)/bin/make-example

make-example: main.c
	$(CC) -o $@ $<

clean: make-example
	$(RM) $<
