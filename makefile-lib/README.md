# Set up classic confinement for a Makefile project

Some snaps need to have access to system resources outside the scope allowed by
strict confinement, and are unable to do this via the available interfaces.
These snaps are configured to use classic confinement.

This guide shows how to enable classic confinement for a snap built with the
`make` plugin. The example project used can be found in this repository.

## Change the confinement to classic

Starting with an existing `snapcraft.yaml` file, change the `confinement` setting to `classic`:

```yaml
confinement: classic
```

This will cause the snap to be built in a way that gives it access to system resources.

## Use linters to identify problems

Snapcraft uses [linters](https://snapcraft.io/docs/linters) to check for issues during builds.
Linters can only be specified in snaps that use the [core22](https://snapcraft.io/docs/base-snaps) base. Warnings are still reported for snaps that use older bases.

Run snapcraft to build the snap. This may produce warnings like the following:

```
Lint warnings:
- classic: bin/example-make-lib: ELF interpreter should be set to '/snap/core22/current/lib64/ld-linux-x86-64.so.2'.
- classic: bin/example-make-lib: ELF rpath should be set to '/snap/core22/current/lib/x86_64-linux-gnu'.
```

If there are many warnings about libraries, the library linter can be disabled so that only classic linter warnings are shown. To do this, add a `lint` section to the `snapcraft.yaml` file:

```yaml
lint:
  ignore:
    - library
```

## Fix linter warnings

In this example, the warnings about the ELF interpreter and rpath can be handled by adding options to the linker in the appropriate build rule of the Makefile:

* `-Wl,-dynamic-linker=/snap/core22/current/lib64/ld-linux-x86-64.so.2`
* `-Wl,-rpath=/snap/core22/current/lib/x86_64-linux-gnu`

This could be done using the `LDFLAGS` environment variable, like this:

```

```
