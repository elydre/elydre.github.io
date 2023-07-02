# Olivine

## Quick Presentation

Olivine is a command line programming language inspired by bash and developed
for profanOS.

Although olivine is developed for the profan environment, it can be used on linux
by setting `PROFANBUILD` to 0, which will disable all profanOS features.

Olivine uses substitution to execute lines of code, for example in the code
`echo Hello !user`, `!user` will be literally replaced by the value of the
variable !user. And the process is the same for function calls and pseudos.

## Main Features

### Quoting

Olivine supports quoting using single quotes `'`. Inside quotes, the string
can contain spaces and will not be split into multiple arguments.

> **Note:** Even words are quoted, variables and subfunctions will still
> be substituted

### Functions Calls

If a line does not start with a keyword, it is considered as a function call.
The function name is the first word of the line and the arguments are the
following words.

```
function arg1 arg2 arg3
function 'arg1 with spaces' arg2
```

Two types of function exist, the internal functions which are in the source
code in C as well as the *classic* functions which are coded in olivine.
(see [Internal Functions](#internal-functions) and [Classic Functions](#classic-functions))

### Variables

Variables are set using the `set` internal function which takes two arguments,
the first one being the name of the variable (without the `!` prefix) and the
second one being the value of the variable.

```
set var 42
```

Variables can be accessed using the `!` prefix.

```
echo !var
```

### Subfunctions Calls

Subfunctions are functions that are called inside a line of code. They are
called using the `!(...)` syntax. Arguments are passed in the same way
as classic function calls

```
echo !(subfunction arg1 arg2)
```
