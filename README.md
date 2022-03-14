# julia_project_basic

This Python package provides functions to check if a Julia project is properly installed and ready to use.

It ensures that registries and packages are installed. It ensures that PyCall.jl is
installed, built, and that the libpython of the running python interpreter is compatible with
the one used to build PyCall.jl

## Install

```sh
pip install julia_project_basic
```

### Examples

#### Simplest use

```python
import os
import julia_project_basic
os.chdir("/path/to/julia/project/")
julia_project_basic.ensure_project_ready()
```

### Function `find`

`find(version_spec=None, check_exe=False, find_all=False, strict=False, env_var=None)`

Calling `find()` will use reasonable defaults.

#### Parameters

-  `env_var` : The environment variable to check for a julia path.
        If this variable is set and the exectuable satisfies `version_spec`, then it will be
        preferred to all other paths. Default: "JULIA".
-  `version_spec` : A [Julia compatibility version specification](https://pkgdocs.julialang.org/v1/compatibility/)
        as a str or object. The returned executable must satisfy this specification. Default: "^1".
-  `strict` : If `True` then prerelease (development) versions will be excluded.
-  `check_exe` : If `True` then check that the path is a Julia by querying it for the version.
        Note that this has already been done for most Julias found when the version was extracted.
-  `find_all` : If `False` skip the locations that are slower to search. If no other exectuables
        are found, the slower locations may be searched anyway. The only slow location is the
        jill-installed location.


### Function `find_or_install`

```
find_or_install(version_spec=None, check_exe=False, find_all=False, strict=False,
                    answer_yes=False, post_question_hook=None,
                    env_var=None)
```

Calling `find_or_install()` will use reasonable defaults.

This function takes all the same parameters as does `find` as well as the following.

#### Parameters

-  `answer_yes` - if `True`, then ask no questions, assume answers are "yes".
-  `post_question_hook` -  a function to run if and after the consumer is asked whether
        to install Julia. This can be used to ask and record more questions rather
        than waiting till after the download. Default: None

