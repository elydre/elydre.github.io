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

### Indentation and Line Breaks

Indentation will be ignored by olivine. Each line of code must be separated
by a line break or a semicolon `;`.

```
echo first line
echo second line

echo first line; echo second line
```

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

Variables can be deleted using the `del` internal function which takes one
argument, the name of the variable to delete.

```
del var
```

Recurcive variables substitution is supported like in PHP.

```
set a 42
set b a

echo !!b
```


### Subfunctions Calls

Subfunctions are functions that are called inside a line of code. They are
called using the `!(...)` syntax. Arguments are passed in the same way
as classic function calls

```
echo !(subfunction arg1 arg2)
```

### Pseudos

Pseudos (aka Nicknames) are replaced between all the substitution steps and
the final call of the function. They have been created in order to simplify
the function calls.

Pseudos are defined with the internal function `pseudo` which takes two
arguments, the first one being the name of the pseudo and the second one
being the value of the pseudo.

```
pseudo pseudo_name value
pseudo tcc 'go /bin/fatpath/tcc'
```

Pseudos are accessible without a prefix like a function call.

```
tcc -c main.c

// Will be automatically replaced by
go /bin/fatpath/tcc -c main.c
```

### Eval Function

The `eval` internal function can be used to evaluate an expression.
The number of arguments and spaces will be ignored.

operators:
- `+` addition
- `-` subtraction
- `*` multiplication
- `/` division
- `^` modulo
- `=` equal (comparison)
- `>` greater than
- `<` less than
- `~` different

```
eval 1+2*(3-1)
eval 42 = 41 + 1
```

### Conditionals

Conditionals are defined using the `IF` keyword followed by the condition.
The `END` keyword must be used to close the conditional.

```
IF !(eval 1 = 1)
    echo 1 is equal to 1
END
```

The `ELSE` keyword can be used after the `IF .. END` block and will be executed
if the condition is false.

```
IF !(eval 1 = 2)
    echo 1 is equal to 2
END; ELSE
    echo 1 is not equal to 2
END
```

> **Note:** The `ELSE` keyword does not have to follow the END of the
> condition but can be separated by code 🫠

### For Loops

For loops are defined using the `FOR` keyword followed by the variable name
and the list of values. The `END` keyword must be used to close the loop.

```
FOR i hi hello hey
    echo !i
END
```

> **Note:** For loops can be slow if the list of values is too long. In this
> case, it is recommended to use a while loop.

### While Loops

While loops are defined using the `WHILE` keyword followed by the condition.
The `END` keyword must be used to close the loop.

```
set i 0
WHILE !(eval !i < 5)
    echo !i
    set i !(eval !i + 1)
END
```

### Break and Continue

The `BREAK` keyword can be used to exit a loop.

```
// Will print 1 2

FOR i 1 2 3 4 5
    IF !(eval !i = 3)
        BREAK
    END
    echo !i
END
```

The `CONTINUE` keyword can be used to skip the current iteration of a loop.

```
// Will print 1 2 4 5

FOR i 1 2 3 4 5
    IF !(eval !i = 3)
        CONTINUE
    END
    echo !i
END
```

### Classic Functions

Classic functions are functions that are coded in olivine. They are defined
using the `FUNC` keyword followed by the name of the function.

A variable named `!#` is automatically set to the number of arguments passed
to the function, and the arguments are accessible using the `!<number>` syntax.

```
FUNC my_function
    echo !# arguments passed
    echo first argument:  !0
    echo second argument: !1
END
```

The function can return a value using the `RETURN` keyword.

```
FUNC double
    RETURN !(eval !0 * 2)
END
```

All the created variables to save the arguments are automatically deleted
after the function call, but the variables created inside the function are
not deleted (see [Variables](#variables)).

### Internal Functions

> **Note:** This section is of no importance if you only use Olivine as your
> shell language.

Internal functions are functions that are coded in C and are compiled with the
olivine binary.

```c
char *if_demo(char **input) {
    // input[0] is the first argument
    // input[1] is the second...

    // The function must return a string. If
    // the function returns NULL, the output
    // will be replaced by an empty string

    return "Hello World";
}

// The function must be registered using the
// internal_functions array:

internal_function_t internal_functions[] = {
    ...
    {"demo", if_demo},
    ...
    {NULL, NULL}
};

```

## Built-in Elements

### Internal Functions

| Name    | Arguments     | Description                                 |
| ------- | ------------- | ------------------------------------------- |
| `echo`  | `...`         | Prints the arguments separated by a space   |
| `upper` | `string`      | Returns the uppercase version of the string |
| `join`  | `...`         | Joins the arguments                         |
| `split` | `string`      | Splits the string                           |
| `set`   | `name var`    | Sets the variable `!name` to `var`          |
| `del`   | `name`        | Deletes the variable `!name`                |
| `debug` |               | Prints all variables, pseudos and functions |
| `eval`  | `expr`        | Evaluates the expression                    |
| `go`    | `binfile`     | Executes the binary file                    |
| `exec`  | `file`        | Executes the file as Olivine code           |
| `cd`    | `dir`         | Changes the current directory               |
| `pseudo`| `name val`    | Creates a pseudo                            |
| `range` | `start end`   | Returns a list of numbers                   |
| `find`  | `-f|-d [dir]` | Returns the content of a directory          |
| `name`  | `path`        | Returns the name of the file                |

### Default Variables

| Name    | Description                            |
| ------- | -------------------------------------- |
| version | The version of Olivine                 |
| profan  | `1` if build for profan, `0` otherwise |
| path    | The current directory                  |
