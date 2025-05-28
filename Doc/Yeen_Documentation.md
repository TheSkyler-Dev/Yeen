# Yeen

## Table of Contents
1. [What is `Yeen`?](#what-is-yeen)
2. [The `Yeen` Philosophy](#the-yeen-philosophy)
3. [Style Conventions](#Yeen-style-conventions)
4. [Syntax at a Glance](#Yeen-syntax-at-a-glance)
    - [Library Inclusions](#library-inclusions)
    - [Variables](#variables)
    - [Basic Arithmetic](#basic-arithmetic)
    - [Data Structures](#data-structures)
    - [Basic I/O](#basic-io)
    - [Template Literals](#template-literals)
    - [Comments](#comments)
5. [Loops](#loops)
6. [Control Flow](#control-flow)
7. [Conditionals](#conditionals)
8. [Functions and Classes](#functions-and-classes)
9. [Asynchronous Code](#asynchronous-code-in-Yeen)
10. [Error Handling](#error-handling)
11. [Syntax Highlighting](#syntax-highlighting)
12. [Alternative Syntax Highlighting Schemes](#alternative-syntax-highlighting-schemes)

--- 

## What is `Yeen`?
`Yeen` is a modern, memory safe and pythonic superset of Java aimed on making the development of JVM applications simpler and less verbose.

## The `Yeen` Philosophy
`Yeen` aims to provide...
- a pythonic, concise, but easy  to understand syntax
- better memory safety

## `Yeen` Style Conventions
Yeen follows the universally recognized style guidelines provided by [Google](https://tinyurl.com/42h9tfy8). I.e. Four spaces instead of `tab`. Furthermore, it is considered good practice to separate variables, expressions, mathematical and logical operators with spaces for better readability. While it's acceptable to follow the C++ standard practice of ending every statement with a semicolon (`;`) or wrap code blocks within classes, functions or loops in curly braces (`{}`), it is generally recommended and better practice to omit those and use blank lines as separators above and below classes, functions and loops instead. While not strictly required, it's good practice to explicitly declare variable types to avoid ambiguous type errors.

## `Yeen` Syntax at a Glance
### Library Inclusions
Libraries are "included" (actually imported) with the `!import` keyword and allows for direct access to components from a library. Here's how to use it:

```Yeen
!import-> "calc"
or
!import-> "pi" from "calc"
```

## Variables
Variables in `Yeen` can have the following data types by default:
- `str` String
- `int` 64-bit Integer
	- `int32` 32-bit Integer
- `dub` 64-bit Double precision floating point with up to 16 decimal points
	- `dub32` 32-bit floating point (up to 7 decimal points)
- `bool` Boolean, can be represented by `1` and `0`, or `true` or `false`. Type must be explicitly declared to use `1` or `0` as boolean values.

Variables are always declared with the `dec` keyword for non-constant variables, and `const` for constant variables. To declare a variable with an explicit data type, the variable name must be followed with `-><datatype>` without spaces. Otherwise, the type will be inferred. You can also declare multiple variables with the same type in a single line

Example usage:

```Yeen
dec myVar = 0 #type inferred as int
dec myBool->bool = 1 #boolean with value 'true'
dec int->x = 9; y = 10
const pi = 3.14159 #inferred as 'dub'
const pi32->dub32 = 3.1415927 #declared as a 32-bit float
```

In `Yeen`, variables of numeric and alphanumeric types (`int`, `int32`, `dub`, `dub32` and `str`) are nullable,  and must be declared as such by type. It's important to note, that `Yeen` won't let you leave variable uninitialized, so you still have to initialize variables, even if they're nullable.

```Yeen
dec myNum->int? = NaN
dec myStr->str? = nil
```

⚠️ **Important!**
if a variable isn't nullable, default values should be used, such as:
- `0` for `int` or `int32`
- `0.0` for `dub` or `dub32`
- `"def"` or `"default"` for `string`
- `0` or `false` for `bool`

#### Interesting Fact about Variables in `Yeen`
While it's not explicitly enforced, it is good practice to use Yoda notation when working with previously declared variables, as that helps in catching assignment errors on variables.

Example:

```Yeen
const pi->dub = 3.14

pi = 3.1415 #only throws an error on runtime
3.1415 = pi #throws an error in the IDE
```
## Basic Arithmetic
`Yeen` uses the standard, widely recognized mathematical operators:
- `+`: Addition
- `-`: Subtraction
- `/`: Division
- `*`: Multiplication
- `%`: Modulo
- `!`: Factorial
- `**` : Exponentiation

Example usage of mathematical operators in `Yeen`:

```Yeen
tell(16 + 16)
tell(16 - 8)
tell(32 / 2)
tell(10 * 10)
tell(1024 % 8)
tell(5!)
tell(2 ** 7)
```

## Data Structures
`Yeen` supports various data structures, such as Arrays `arr`, Dictionaries `dict` and object collections `col`. Object collections store parameterized objects similar to a JSON file:

```Yeen
people->col = {
    person1:
        "Name": "Jane Doe",
        "Age": 25,
        "Occupation": "Software engineer"
    
    person2:
        "Name": "John Doe",
        "Age": 27,
        "Occupation": "Police Lieutenant"
}
```

## Basic I/O
`Yeen` handles input and output similarly to other languages, but with its own syntax. It uses the standard `tell()` function for output and `readln()` function for input, which supports input prompts enclosed in double or single quotes within the parentheses.

```Yeen
dec myVar->str = "default"
myVar = readln("Enter your Name: ")
tell(myVar)
```

For required input, the `.require` marker can be used.

```Yeen
dec name->str = "default"
name = readln("Please enter your name: ").require
```

## Template Literals
`Yeen` supports template literals. To use them, the string must be enclosed in single quotes. You can use template literals to insert variables and expressions directly into a string. Expression must be enclosed in curly braces.

```Yeen
dec int->x = 9; y = 10
dec name->str = "Jane Doe"
dec example->str = '$name says that $x + $y equals ${x + y}.'
tell(example)
```

## Comments
- `#` Normal comment
- `#!` Multi-line comment

## Loops
`Yeen` supports your usual types of loops: `while`-loops, `do...while` loops and `for` loops. These essentially work the same as in other programming languages, but with some differences in syntax. Numeric variables in `Yeen` support incrementing values (`++`) and decrementing values (`--`). The step for increment/decrement is 1. `for` loops also support ranges.

`while` loop:
```Yeen
while(true):
    #some code
endwhile
```

`do-while` loop:
```Yeen
do:
    #some code
while(<condition>)
```

`for` loop:
```Yeen
for(dec i->int = 0; i < 10; i++):
    #some code (e.g. a list iterator)
endfor

#or

for i in range 0..10 step 0.5:
    #some code
endfor
```

## Control Flow
`Yeen` supports the usual control flow structures like `if`/`elif`/`else` and switch statements (`sw`). `if/else` statements must end with the `endif` keyword and switch statements have to end with the `endsw`keyword. For single-line `if` statements, the `endif` keyword can be omitted.

`if/else` statement:

```Yeen
if (<condition>):
    #some code
else:
    #some code
endif
```

Example usage:
```Yeen
dec age->int = readln("Enter your age: ").require
if (age < 18):
    tell("You are a minor.")
elif (age >= 18 && age < 65):
    tell("You are an adult.")
else:
    tell("You are a senior citizen.")
endif
```

switch statement:

```Yeen
sw (<condition>):
    case 1:
        #case 1 code
        
    ...
    
    def:
        #default case
endsw
```

## Conditionals
`Yeen` generally supports all logic operators like AND (`&&`), OR (`||`) etc. and use the generally recognized symbols for doing so. These can also be used in bitwise operations. Additionally, Elvis operators (`:?`) are also supported by `Yeen`. Operators like `&&` and `||` can also be used in control flow when you need to cover a condition with a single code block or need two conditions to be true for a certain block of code to execute.

Logical operators in control flow:

```Yeen
dec num1->int = 0
dec num2->int = 0
num1 = readln("Enter num 1: ")
num2 = readln("Enter num 2: ")
if(num1 == 1 && num2 == 0):
    #some code here
endif
```

Elvis operator example:

```Yeen
dec username->str? = nil
dec displayName->str? = !username.empty() ? username : "Guest"
```

## Functions and Classes
- Functions are declared with the `fun` keyword and must end with the `endfun` keyword. Data is returned with the `ack` keyword, which "acknowledges" and returns a value.
- Classes are declared with the `class` keyword and must end with the `endclass` keyword.
#### `Yeen` function example

```Yeen
fun myFunc():
	#function contents
	ack none
endfun
```

#### `Yeen` class example

```Yeen
class myClass():
	constr:{
		#constructor
	}
	
	pub:{
		#public methods
	}
	
	prot:{
		#protected methods
	}
	
	priv:{
		#private methods
	}
endclass
```

Example usage:

```Yeen
class Person():
    constr(name->str, age->int):
        self.name = name
        self.age = age

    pub:
        fun greet():
            tell("Hello, my name is $self.name and I am $self.age years old.")
        endfun
endclass

dec john->Person = Person("John", 30)
john.greet()
```

External classes are called by the main source file through the `!import->` flag. Once included, you can call the public functions of the class.

## Asynchronous Code in `Yeen`
`Yeen` runs synchronously by default. However, you can declare asynchronous code blocks when needed, using the `desync`, `resync` and `expect` keywords. Here's an example:

```Yeen
desync fun myAsyncFunc():
    #some code
    dec dynamicData->dub = dynData
    ack dynamicData
resync
dec data->dub = 0.0
expect data = myAsyncfunc()
```

Note that the block has to start with `desync` and ends with `resync`. Alternatively, the `resync-fun` keyword can be used to end a desync function.

## Error handling

`Yeen`, by default, already handles errors fairly well with concise error messages, however, you may want to handle possible errors in your programs more gracefully. That's where the `try` `catch` statement comes in. it works no different than in other programming languages, however providing an error code and error message works slightly differently:

```Yeen
try:
    #some code here
catch:
    throw(err(ecode(), "An error occured"))
```

Here, the standard function `err()` (`err(prefix, error message)`) lets you build a custom error message, while the `ecode()` function generates an error code. Here, the resulting error message would have whatever error code `ecode()`returns, set as the prefix. For handling variables with the values `nil` or `NaN`, the checking methods `isNaN()` and `isNil()` are used. These methods can also be used within `if-else` statements. Alternatively, `isEmpty()` can be used:

```Yeen
dec myStr->str = nil
if(myStr.isNil()):
    throw(err(ecode(), "Error message"))
endif

#or

if(myStr.isEmpty()):
    throw(err(ecode(), "Error message"))
endif
```
## Syntax highlighting

`Yeen` can use any widely known syntax highlighting scheme, but the standard syntax highlighting for `Yeen` takes inspiration from the syntax highlighting used for Swift in the XCode modern Dark theme for VSCode:

- Keywords (`fun`, `class`, etc.): Persian Pink (#F77FBE)
- Variables and constants : White #FFFFFF(dark mode), Black #000000 (light mode)
- Strings: Salmon Red (#FA8072)
- Template literals (`$`, `${}`) Yellow (#FFFF00)
- Function names: Steel Blue (#4682B4)
- Class names: Light Steel Blue (#B0C4DE)
- Data types: Lavender (#E6E6FA)
- Unused variables and functions: Navy Gray (#656B83)

**`Yeen` also resolves invisible characters:**
- Zero-Width Space: Resolved to`<ZWSP>` (Red (#FF0000) translucent background and underline)
- Whitespace: Resolved to `<WSPACE>` (Orange (#FFA500) translucent background and underline)
- EM Space: Resolved to `<EM>` (Fluorescent Yellow (#CCFF00) translucent background and underline)

## Alternative Syntax Highlighting Schemes
`Yeen` offers alternative syntax highlighting color schemes that are color corrected for colorblindness (primarily protanopia, deuteranopia and tritanopia). These can be set and adjusted as needed in the settings of the official `Fern` plugin in your IDE. Here are those themes:

### Protanopia

- Keywords (`fun`, `class`, etc.): Bright Blue (#0088FF)
- Variables and constants : White #FFFFFF(dark mode), Black #000000 (light mode)
- Strings: Yellow (#FFDD00)
- Template literals (`$`, `${}`) Cyan (#00FFFF)
- Function names: Deep Blue (#0044AA)
- Class names: Light Blue (#88CCFF)
- Data types: Pale Yellow (#FFFFCC)
- Unused variables and functions: Gray (#888888)

**invisible characters:**
- Zero-Width Space: Resolved to `<ZWSP>` with contrast underline, Bold text
- Whitespace: Resolved to `<WSPACE>` with contrast underline, Bold text
- EM Space: Resolved to `<EM>` with contrast underline, Bold text
### Deuteranopia

- Keywords (`fun`, `class`, etc.): Purple (#8800FF)
- Variables and constants : White #FFFFFF(dark mode), Black #000000 (light mode)
- Strings: Sky Blue (#00CCFF)
- Template literals (`$`, `${}`) Bright Yellow (#FFEE00)
- Function names: Navy (#000088)
- Class names: Light Purple (#BB88FF)
- Data types: Light Gray (#DDDDDD)
- Unused variables and functions: Dark Gray (#666666)

**invisible characters:**
- Zero-Width Space: Resolved to `<ZWSP>` with contrast underline, Bold text
- Whitespace: Resolved to `<WSPACE>` with contrast underline, Bold text
- EM Space: Resolved to `<EM>` with contrast underline, Bold text
### Tritanopia

- Keywords (`fun`, `class`, etc.): Magenta (#FF00FF)
- Variables and constants : White #FFFFFF(dark mode), Black #000000 (light mode)
- Strings: Red (#FF0000)
- Template literals (`$`, `${}`) Bright Green (#00FF00)
- Function names: Dark Red (#990000)
- Class names: Pink (#FF88FF)
- Data types: Very Light Green (#DDFFDD)
- Unused variables and functions: Olive (#888800)

**invisible characters:**
- Zero-Width Space: Resolved to `<ZWSP>` with contrast underline, Bold text
- Whitespace: Resolved to `<WSPACE>` with contrast underline, Bold text
- EM Space: Resolved to `<EM>` with contrast underline, Bold text

---

:copyright: **TheSkyler-Dev, Documentation licensed under CC BY-SA 4.0 International**
