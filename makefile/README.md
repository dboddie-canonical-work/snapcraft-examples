# Creating a snap for a Makefile project

This guide shows how to create a snap for a Makefile project, using a simple
project as an example.

You will need to [install Snapcraft](https://snapcraft.io/docs/snapcraft-setup)
before following these steps.

## Clone and build the example

Use `git` to clone this repository into a new directory and make it the
current working directory.

Test that the project builds in the normal way by running `make`. This should
give output like the
following:

```
$ make
cc -o make-example main.c
```

The `make-example` executable should now be found in the current directory.
You can run it to test that it works:

```
$ ./make-example
It worked!
```
Clean the working directory after testing:

```
$ make clean
rm -f make-example
```

With a working

## Create a snapcraft project file

In the project directory, run the `snapcraft` tool to create an initial `snapcraft.yaml` project file:

```bash
$ snapcraft init
```

This will create a subdirectory called `snap` containing the `snapcraft.yaml` file with some default
definitions. Modify

```yaml
name: make-example
base: core22
version: '0.1'
summary: An example snap for a Makefile project
description: |
  Shows how to create a snap for an application that uses a Makefile for
  build and installation.

grade: devel
confinement: strict

apps:
  make-example:
    command: bin/make-example

parts:
  make-example-part:
    plugin: make
    source: .
```
