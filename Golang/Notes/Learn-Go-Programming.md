# Learn Go Programming

## Overview

### Features of Go Programming

* Support for environment adopting patterns similar to dynamic languages. For example, type inference (x := 0 is valid declaration of a variable x of type int)
* Compilation time is fast.
* Inbuilt concurrency support: lightweight processes (via go routines), channels, select statement.
* Go programs are simple, concise, and safe.
* Support for Interfaces and Type embedding.
* Production of statically linked native binaries without external dependencies.

### Features Excluded Intentionally

* Support for type inheritance
* Support for method or operator overloading
* Support for circular dependencies among packages
* Support for pointer arithmetic
* Support for assertions
* Support for generic programming

## Program Structure

* Package Declaration
* Import Packages
* Functions
* Variables
* Statements and Expressions
* Comments

## Basic Syntax

### Tokens in Go

A token is either a keyword, an identifier, a constant, a string literal, or a symbol.

### Line Separator

The Go compiler internally places “;” as the statement terminator to indicate the end of one logical entity.

### Comments

Comments start with /* and terminates with the characters */

### Identifiers

identifier = letter { letter | unicode_digit }

## Data Types

### Integer Types

| uint8 | uint16 |  uint32 | uint64 | int8 | int16 | int32 | int64 |

### Floating Types

| float32 | float64 | complex64 (Complex numbers with float32 real and imaginary parts) | complex128 |

### Other Numeric Types

| byte | rune (same as int32) | unit | int | uintptr |

## Variables

Each variable in Go has a specific type, which determines the size and layout of the variable's memory, the range of values that can be stored within that memory, and the set of operations that can be applied to the variable.

Upper and lowercase letters are distinct because Go is case-sensitive.

### Variable Definition in Go

```go
var variable_list optional_data_type;
var i, j, k int;
i = 1, j = 2;
```

Variables with static storage duration are implicitly initialized with nil (all bytes have the value 0).

### Static Type Declaration in Go

A static type variable declaration provides assurance to the compiler that there is one variable available with the given type and name so that the compiler can proceed for further compilation without requiring the complete detail of the variable. A variable declaration has its meaning at the time of compilation only, the compiler needs the actual variable declaration at the time of linking of the program.

### Dynamic Type Declaration / Type Inference in Go

A dynamic type variable declaration requires the compiler to interpret the type of the variable based on the value passed to it. The compiler does not require a variable to have type statically as a necessary requirement.

```go
y := 42
```

### Mixed Variable Declaration in Go

```go
var a, b, c = 3, 5, "foo"
```

### The lvalues and the rvalues in Go

An *lvalue* may appear as either the left-hand or right-hand side of an assignment. An *rvalue* is an expression that cannot have a value assigned to it which means an rvalue may appear on the right- but not left-hand side of an assignment.

## Constants

### Integer Literals

An integer literal can have a suffix that is a combination of U(u) and L(l), for unsigned and long, respectively.

```go
212         /* Legal */
215u        /* Legal */
0xFeeL      /* Legal */
078         /* Illegal: 8 is not an octal digit */
032UU       /* Illegal: cannot repeat a suffix */
```

### Floating-point Literals

```go
3.14159       /* Legal */
314159E-5L    /* Legal */
510E          /* Illegal: incomplete exponent */
210f          /* Illegal: no decimal or exponent */
.e55          /* Illegal: missing integer or fraction */
```

### String Literals in Go

String literals or constants are enclosed in double quotes "".

You can break a long line into multiple lines using string literals and separating them using whitespaces.

### The *const* Keyword

```go
const variable type = value;
```

## Operators

### Arithmetic Operation

| + | - | * | / | % | ++ | -- |

### Relational Operators

| == | != | > | < | >= | <= |

### Logical Operators

| && | || | ! |

### Bitwise Operators

| & | | | ^ | ~ | << | >> (Arithmetic Right Shift) |

### Assignment Operators

| = | += | -= | *= | /= | %= | <<= | >>= | &= | ^= | |= |

### Miscellaneous Operators

| & (Return the address of a variable) | * (Pointer to a variable) |

## Decision Making

### if statement

```go
if(boolean_expression) {
   /* statement(s) will execute if the boolean expression is true */
}
```

### if...else statement

```go
if(boolean_expression) {
   /* statement(s) will execute if the boolean expression is true */
} else {
   /* statement(s) will execute if the boolean expression is false */
}
```

### The Switch Statement

No **break** is needed in the case statement and default case.

#### Expression Switch

```go
switch(boolean-expression or integral type){
   case boolean-expression or integral type :
      statement(s);
   case boolean-expression or integral type :
      statement(s);
   /* you can have any number of case statements */
   default : /* Optional */
      statement(s);
}
```

#### Type Switch

```go
switch x.(type){
   case type:
      statement(s);
   case type:
      statement(s);
   /* you can have any number of case statements */
   default: /* Optional */
      statement(s);
}
```

### The Select Statement

The **type** for a case must be the a communication channel operation.

```go
select {
   case communication clause  :
      statement(s);
   case communication clause  :
      statement(s);
   /* you can have any number of case statements */
   default : /* Optional */
      statement(s);
}
```

## Loops

### for Loop

```go
for [condition |  ( init; condition; increment ) | Range] {
   statement(s);
}
```

### break statement

It terminates a for loop or switch statement and transfers execution to the statement immediately following the for loop or switch.

### continue statement

It causes the loop to skip the remainder of its body and immediately retest its condition prior to reiterating.

### goto statement

It transfers control to the labeled statement.

## Functions

Every Go program has at least one function, which is main().

A function **declaration** tells the compiler about a function name, return type, and parameters. A function **definition** provides the actual body of the function.

### Defining a Function

```go
func function_name( [parameter list] ) [return_types]
{
   body of the function
}
```

### Function Arguments

#### Call by value

By default, Go programming language uses **call by value** method to pass arguments.

### Call by reference

The **call by reference** method of passing arguments to a function copies the address of an argument into the formal parameter.

### Function Usage

#### Function as Value

Go programming language provides the flexibility to create functions on the fly and use them as values.

```go
getSquareRoot := func(x float64) float64 {
    return math.Sqrt(x)
}
```

#### Function Closures

Go programming language supports anonymous functions which can acts as function closures. Anonymous functions are used when we want to define a function inline without passing any name to it.

```go
func getSequence() func() int {
   i:=0
   return func() int {
      i+=1
      return i
   }
}

func main(){
   /* nextNumber is now a function with i as 0 */
   nextNumber := getSequence()
   /* invoke nextNumber to increase i by 1 and return the same */
   fmt.Println(nextNumber())
   fmt.Println(nextNumber())
   fmt.Println(nextNumber())
}
```

When the above code is compiled and executed, it produces the following result −

```text
1
2
3
```

#### Method

In method declaration syntax, a "receiver" is present to represent the container of the function. This receiver can be used to call a function using "." operator.

```go
func (variable_name variable_data_type) function_name() [return_type] {
    /* function body*/
}
```

## Scope Rules

### Local Variables

Local variables are not known to functions outside their own.

### Global Variables

A program can have the same name for local and global variables but the value of the local variable inside a function takes preference.

### Formal Parameters

Formal parameters are treated as local variables with-in that function and they take preference over the global variables.