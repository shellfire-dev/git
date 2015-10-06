# `git`: functions module for [shellfire]

This module provides a simple set of wrapper functions for making it more pleasant to work with `git`.

## Compatibility

* Current `HEAD` is compatible with [shellfire] release [`release_2015.0117.1750-1`](https://github.com/shellfire-dev/shellfire/releases/tag/release_2015.0117.1750-1).

## Overview

Usage couldn't be simpler. Just pick a function. Please note that most functions are not currently documented.

## Importing

To import this module, add a git submodule to your repository. From the root of your git repository in the terminal, type:-

```bash
mkdir -p lib/shellfire
cd lib/shellfire
git submodule add "https://github.com/shellfire-dev/git.git"
cd -
git submodule init --update
```

You may need to change the url `https://github.com/shellfire-dev/git.git` above if using a fork.

You will also need to add paths - include the module [paths.d].


## Namespace `git`

This namespace contains useful functions wrapping `git`.

### To use in code

If calling from another [shellfire] module, add to your shell code the line
```bash
core_usesIn git
```
in the global scope (ie outside of any functions). A good convention is to put it above any function that depends on functions in this module. If using it directly in a program, put this line _inside_ the `_program()` function:-

```bash
_program()
{
	core_usesIn git
	…
}
```

### Functions

***
#### `git_mostRecentCommit()`

|Parameter|Value|Optional|
|---------|-----|--------|
|`gitRepositoryPath`|Path to a git repository (or submodule), ie a path with a `.git` folder or file.|_No_|

The function prints to standard out, without a trailing new line, the most recent commit hash (a full hash is returned, eg `166bcda6abd46e7e1f0107ad4006323a9398afd3`). A typical usage might be:-

```bash
lastCommit="$(git_mostRecentCommit "/path/to/repo/folder")"
```

Does not check the path exists.

***
##### `git_commitToTagOrCommit`

|Parameter|Value|Optional|
|---------|-----|--------|
|`gitRepositoryPath`|Path to a git repository (or submodule), ie a path with a `.git` folder or file.|_No_|
|`commit`|A commit hash (eg retrieved with `git_mostRecentCommit()`).|_No_|

The function prints to standard out, without a trailing new line, the tag that that exaxtly matches the `commit` hash, or, if not present, returns `commit`. A typical usage might be:-

```bash
tagOrCommit="$(git_commitToTagOrCommit "/path/to/repo/folder" "166bcda6abd46e7e1f0107ad4006323a9398afd3")"
```

***
#### `git_withOutputSilencedIfQuiet()`

|Parameter|Value|Optional|
|---------|-----|--------|
|`verbosityLevel`|A number such as `1`, `2`, etc that matches `--verbosity` on the command line.|_No_|
|`gitCommand`|Git command, eg `clean`|_No_|
|`gitCommandArguments`|Zero or more arguments to pass to `gitCommand`|_Yes_|

Helper function to only make git commands noisy if a verbosity threshold is met or exceeded. Runs `gitComand [gitCommandArguments]` if `verbosityLevel` is matched or exceeded, otherwise runs `gitComand -q [gitCommandArguments]`. `gitCommand` must be able to accept `-q` (not all commands do).


[swaddle]: https://github.com/raphaelcohn/swaddle "Swaddle homepage"
[shellfire]: https://github.com/shellfire-dev "shellfire homepage"
[core]: https://github.com/shellfire-dev/core "shellfire core module homepage"
[paths.d]: https://github.com/shellfire-dev/paths.d "paths.d shellfire module homepage"
[github api]: https://github.com/shellfire-dev/github "github shellfire module homepage"
[jsonwriter]: https://github.com/shellfire-dev/jsonwriter "jsonwriter shellfire module homepage"
[jsonreader]: https://github.com/shellfire-dev/jsonreader "jsonreader shellfire module homepage"
[urlencode]: https://github.com/shellfire-dev/urlencode "urlencode shellfire module homepage"
[unicode]: https://github.com/shellfire-dev/unicode "unicode shellfire module homepage"
[version]: https://github.com/shellfire-dev/version "version shellfire module homepage"