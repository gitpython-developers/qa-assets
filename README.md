# gitpython-developers qa-assets

This repository contains files used as inputs for automated testing of gitpython-developers owned projects. Currently,
only GitPython's OSS-Fuzz related blobs are housed here.

For information about GitPython's OSS-Fuzz integration and fuzz tests, please refer
to [GitPython's fuzzing/README.md](https://github.com/gitpython-developers/GitPython/blob/main/fuzzing/README.md)

For details about the contents of this repository, continue reading.

## Files & Directories Overview

### Seed Corpora (`gitpython/corpora/`)

Contains one subdirectory per fuzz target, each containing a set of minimal test inputs (called a "corpus") that enable
the fuzzing engine to generate some initial coverage that it can build on.

### Dictionaries (`gitpython/dictionaries/`)

Provides hints to the fuzzing engine about inputs that might trigger unique code paths. Each fuzz target may have a
corresponding `.dict` file. For information about dictionary syntax, refer to
the [LibFuzzer documentation on the subject](https://llvm.org/docs/LibFuzzer.html#dictionaries).

**Things to Know**:

- OSS-Fuzz loads dictionary files per fuzz target if one exists with the same name, all others are ignored.
- Most entries in the dictionary files found here are escaped hex or Unicode values that were recommended by the fuzzing
  engine after previous runs.
- A default set of dictionary entries should be created for all fuzz targets as part of the build process, regardless of
  an existing file here.
- Development or updates to dictionaries should reflect the varied formats and edge cases relevant to the
  functionalities under test.
- Example dictionaries (some of which are used to build the default dictionaries mentioned above) can be found here:
  - [AFL++ dictionary repository](https://github.com/AFLplusplus/AFLplusplus/tree/stable/dictionaries#readme)
  - [Google/fuzzing dictionary repository](https://github.com/google/fuzzing/tree/master/dictionaries)

