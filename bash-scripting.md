# Overview

## Setup

```
#!/usr/bin/env bash

set -u
set -e
set -o pipefail

USAGE="Usage: $(basename "$0") gpr[wbaskvh]

ARGUMENTS
-g              : description of the argument

DEPENDENCIES
aws (cli)

EXAMPLES
Some nice example implementations of this script
"

```
* `set -u`: Treat unset variables as an error
* `set -e`: Exit on an error that isn't scoped by a loop or if statement
* `set -x`: Show all of the expanded commands in a script as they happen
* `set -o pipefail`: Exit if any command in a pipeline (like if statement) fails

## Parameters

Useful link: https://www.shellscript.sh/tips/getopts/

```
MY_VAR=false

while getopts 'g:n:wvh' OPTION; do
case $OPTION in
    g)  GIT_REPO="$OPTARG"          ;;
    n)  NAME="$OPTARG"              ;;
    w)  MY_VAR=true                 ;;
    v)  set -x;                     ;;
    [h?]) echo "$USAGE"; exit 0     ;;
esac
done
shift "$((OPTIND - 1))"

: "${GIT_REPO:?}"
: "${NAME:?}"
```
* `'g:n:wvh'`: names the flags for this script. Single ones require input,
  grouped ones are just flags (like `tar -xvf my.tar`
* `g)  GIT_REPO="$OPTARG";;`: Uses the passed value to set an internal variable
* `v)  set -x;`: sets the `-x` flag to make this verbose
* `[h?]) echo "$USAGE";`: outputs the contents of `USAGE`
* `shift "$((OPTIND - 1))"`: gets rid of the arguments that have been parsed
  leaving what's left for $1
* `: "${NAME:?}"`: test the named variable has been set up by the script
  variables

## Looping

while
```
while [ <some test> ]; do
    <commands>
done
```

for
```
for var in <list>
do
<commands>
done
```

`break` and `continue` work


source: https://ryanstutorials.net/bash-scripting-tutorial/bash-loops.php

## If statements


```
```
