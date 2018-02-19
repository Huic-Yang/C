# Functions and Program Structure

## Basic of Functions

```C
return_type function_name(argument declarations) {
    declarations and statements
        
    return expression;
}
```

## Functions Returning Non-Integers

## External Variables

* A C program consists of a set of external objects, which are either variables or functions.
* External variables are defined outside of functions.
* Functions themselves are always external, because C does not allow functions to be defined inside other functions.
* External variables are globally accessible.
* Automatic variables are internal to a function. They come into existence when the function is entered, and disappear when it is left.
* External variables are permanent.



## Scope Rules

* The scope of a name is the part of the program within which the name can be used.
* For an automatic variable declared at the beginning of a function, the scope is the function in which the name is declared.
* Local variables of the same name in different functions are unrelated.
* Parameters of the function are in effect local variables.
* The scope of an external variables or a function lasts from the point at which it is declared to the end of the file being compiled.
* The *definition* of the external variables causes storage to be set aside, and also serve as the declaration for the rest of that source file.

```C
int external_var;
double external_arr[MAXSIZE];
```

* The *declaration* doesn't create the variables or reserve storage for them

```C
extern int external_var;
double external_arr[MAXSIZE];
```

* There must be only one definition of an external variable among all the files that make up the source program.
* Other files may contain $\texttt{extern}$ to access it.
* Initialization of an external variables goes only with the definition.



## Header Files

* Those definitions and declarations shared among the files can be placed in a *header file*.

## Static Variables

