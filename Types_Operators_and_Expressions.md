# Types, Operators and Expressions

## Variable Names

some restriction on the names of variables and symbolic constants:

* made up of **letters**, **digits** and **underscore**
* the first character must be a **letter** or **underscore**
* upper case and lower case letters are distinct
* cannot use **keywords** as variables names

## Data Types and Sizes

| $\texttt{char}$   | a single byte, capable of holding one character in the local character set. |
| ----------------- | ------------------------------------------------------------ |
| $\texttt{int}$    | **an integer, typically reflecting the natural size of integers on the host machine.** |
| $\texttt{double}$ | **double-precision floating point.**                         |
| $\texttt{float}$  | **single-precision floating point.**                         |

### Qualifiers

#### $\texttt{short}$ and $\texttt{long}$

* $\texttt{short int}$
* $\texttt{long int}$ 
* $\texttt{long double}$

$\texttt{short int}$(16 bits) $\le$ $\texttt{int}$(16 or 32 bits) $\le$ $\texttt{long int}$(32 bits)

#### $\texttt{signed}$ and $\texttt{unsigned}$

* $\texttt{signed char}$
* $\texttt{unsigned char}$
* $\texttt{signed (long/short) int}$
* $\texttt{unsigned (long/short) int}$

Whether plain chars are signed are signed or unsigned is machine-dependent, but printable characters are always positive.

> The standard headers $\texttt{<limits.h>}$ and $\texttt{<float.h>}$ contain symbolic constants for all of these sizes, along with other properties of the machine and compilers.

## Constants

* integer constants

```C
int int_constant = 12345;
```

* long constants

```C
long long_constant = 123456789L;
long long_constant_2 = 123456788l;
```

* unsigned constants

```C
unsigned unsigned_constant = 201802152330uL;
```

* float-point constants

```C
double d1 = 3.14;
double d2 = 3e8;
float f1 = 3.14f;
float f2 = 3.14F;
double d3 = 3.14l;
double d4 = 3e8L;
```

* octal constants

```C
char char_A = 0101u;
int octal = 02333;
```

* hexadecimal constants

```C
int hex1 = 0x1f;
unsigned hex2 = 0x1fu;
long hex3 = 0x1fl;
unsigned long hex4 = 0xful;
```

* character constants

```C
char ch1 = 65;
char ch2 = 'A';
char ch3 = '\101';
char ch4 = '\x41';
	
printf("%c %c %c %c\n", ch1, ch2, ch3, ch4);
```

* set of escape sequence:
  * $\texttt{\a}$ 	alert (bell) character
  * $\texttt{\b}$    backspace
  * $\texttt{\f}$    formfeed
  * $\texttt{\n}$    newline
  * $\texttt{\r}$    carriage return
  * $\texttt{\t}$    horizontal tab
  * $\texttt{\v}$    vertical tab
  * $\texttt{\\\\}$    backslash
  * $\texttt{\?}$    question mark
  * $\texttt{\'}$    single quote
  * $\texttt{\"}$    double quote
  * $\texttt{\ooo}$ octal number
  * $\texttt{\xhh}$ hexadecimal number    
* constant expression

```C
#define MAX_CAPACITY 10000;
'x';
"x";
enum escapes {
  	BELL = '\a', BACKSPACE = '\b', TAB = '\t',
	NEWLINE = '\n', VTAB = '\v', RETURN = '\r'
};
```

## Declarations

* all variables must be declared before use.
* external and static variables are initialized to zero by default
* automatic variables for which there is no explicit initializer have undefined values
* $\texttt{const}$ specifies that variable will not be changed

## Arithmetic Operators

$\texttt{+, -, *, /, %}$

* $\texttt{%}$ cannot be applied to $\texttt{float}$ or $\texttt{double}$
* The direction of truncation for $\texttt{/}$ and the sign of the result for $\texttt{%}$ are machine-dependent for negative operands, as is the action taken on overflow or underflow
* Arithmetic operators associate left to right
* $\texttt{%}$ $\le$ $\texttt{+, -}$ $\le$ $\texttt{*, /}$

## Relational and Logical Operators

relational operators: $\texttt{>, >=, <, <=}$

equality operators: $\texttt{==, !=}$

* relational operators have lower precedence than arithmetic operators

logical operators: $\texttt{&&, ||, !}$

* The precedence of $\texttt{&&}$ is higher than $\texttt{||}$
* logical operators < equality operators < relation operators
* $\texttt{!}$ converts a non-zero operand into 0 and a zero operand into 1.

## Type conversions

### Automatic Conversions

* $\texttt{char}$ is a small integer, so it may be freely used in arithmetic
* Whether a conversion from a $\texttt{char}$ to a $\texttt{int}$ produces a signed or unsigned quantities is machine-dependent.
* Any characters in the machine's standard printing character set will never be negative.
* Relational expressions and logical expressions connected by $\texttt{&&}$ or $\texttt{||}$ are defined to have value $\texttt{1}$ if true, and $\texttt{0}$ if false.
* Functions may return non-zero value for true.
* implicit arithmetic conversions without unsigned operands
  * if either operand is $\texttt{long double}$, convert the other to $\texttt{long double}$.
  * Otherwise, if either operand is $\texttt{double}$, convert the other to $\texttt{double}$.
  * Otherwise, if either operand is $\texttt{float}$, convert the other to $\texttt{float}$.
  * Otherwise, convert $\texttt{char}$ and $\texttt{short}$ to $\texttt{int}$.
  * Then, if either operand is $\texttt{long}$, convert the other to $\texttt{long}$
* conversions with $\texttt{unsigned}$ operands is complicated
* conversions take place across assignments.
  * The value of right side is converted the type of the left, which is the type of the result.
  * Longer integers are converted to shorted ones or to $\texttt{chars}$ by dropping the excess high-order bits.
  * $\texttt{float}$ to $\texttt{int}$ causes truncation of any fractional part.
  * When $\texttt{double}$ is converted to $\texttt{float}$, whether the value is rounded or truncated is implementation-dependent.
* conversions in function
  * Since an argument of a function call is an expression, type conversions also take place when arguments are passed to functions
  * In the absence of a function prototype, $\texttt{char}$ and $\texttt{short}$ become $\texttt{int}$, and $\texttt{float}$ becomes $\texttt{double}$.

### Forced Conversions

$\texttt{}$$\texttt{}$$\texttt{}$$\texttt{}$$\texttt{(type name) expression}$

## Increment and Decrement Operators

$\texttt{++, --}$

* prefix operators increment variables before their value is used.
* postfix operators decrement variables after their value is used.
* The increment and decrement operators can only be applied to variables.

```C
int i = 1, j = 2;
int k = (i + j)++; // error: lvalue required as increment operand.
```

## Bitwise Operators

| operators     | state                    |      |      |
| ------------- | ------------------------ | ---- | ---- |
| $\texttt{&}$  | bitwise AND              |      |      |
| $\texttt{|}$  | bitwise inclusive OR     |      |      |
| $\texttt{^}$  | bitwise exlusive OR      |      |      |
| $\texttt{<<}$ | left shift               |      |      |
| $\texttt{>>}$ | right shift              |      |      |
| $\texttt{~}$  | one's compliment (unary) |      |      |

* right shift
  * right shift a signed quantity will fill with sign bits ("arithmetic shift") on some machines
  * and with 0-bits ("logical shift") on others.

```C
/* getbits: get n bits from position p */
unsigned getbits(unsigned x, int p, int n) {
	return (x >> p + 1 - n) & ~(~0 << n);
}
```

## Assignment Operators and Expressions

If $expr_1$ and $exper_2$ are expressions, then
$$
expr_1 \  op= expr_2
$$
is equivalent to
$$
expr_1 = (expr_1)\  op \  (expr_2)
$$
where $op$ is one of
$$
\texttt{+ - * / % << >> & ^ |}.
$$

## Conditional Expressions

```C
if (a > b)
    z = a;
else 
    z = b;

z = (a > b)? a : b;

float f;
int n;
(n > 0)? f : n; // is of type float regradless of whether n is positive.
```

## Precedence and Order of Evaluation

| OPERATORS                                               | ASSOCIATIVITY |
| ------------------------------------------------------- | ------------- |
| $\texttt{()  []  ->  .}$                                | left to right |
| $\texttt{!  ~  ++  --  +  -  *  &  (type)  sizeof}$     | right to left |
| $\texttt{*  /  %}$                                      | left to right |
| $\texttt{+  -}$                                         | left to right |
| $\texttt{<<  >>}$                                       | left to right |
| $\texttt{<  <=  >  >=}$                                 | left to right |
| $\texttt{==  !=}$                                       | left to right |
| $\texttt{&}$                                            | left to right |
| $\texttt{^}$                                            | left to right |
| $\texttt{|}$                                            | left to right |
| $\texttt{&&}$                                           | left to right |
| $\texttt{||}$                                           | left to right |
| $\texttt{?:}$                                           | right to left |
| $\texttt{=   +=  -=  *=  /=  %=  &=  ^=  |=  <<=  >>=}$ | right to left |
| $\texttt{,}$                                            | left to right |

* Unary $\texttt{+, -,}$ and $\texttt{*}$ have higher precedence than the binary forms.

