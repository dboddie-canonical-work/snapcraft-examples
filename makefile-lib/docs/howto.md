# Creating a snap for a Makefile project

This guide shows how to create a snap for a Makefile project, using a simple
project as an example.

You will need to install Snapcraft before following these steps.

## The project files

Create a new project directory and make it the current working directory.
In the new directory, create a source file called `main.c`:

```C
#include <stdio.h>

int main(int argc, char *argv[])
{
    printf("It worked!\n");
    return 0;
}
```

Create a `Makefile`:
```make
.PHONY: all

all: make-example

install: make-example
	install -D make-example $(DESTDIR)/bin/make-example

make-example: main.c
	$(CC) -o $@ $<

clean: make-example
	$(RM) $<
```

Test that the project builds in the normal way by running `make`:
```
$ $ make
cc -o make-example main.c
```

This should produce the `make-example` executable. You can test it and clean the working directory.

## Create a snapcraft project file

In the project directory, run the `snapcraft` tool to create an initial `snapcraft.yaml` project file:

```bash
$ snapcraft init
```

This will create a subdirectory called `snap` containing the `snapcraft.yaml` file with some default
definitions.

```yaml

```


