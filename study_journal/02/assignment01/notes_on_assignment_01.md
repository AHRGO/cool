# Notes on Assignment 01
In this first assignment, we must implement a Lexical Analyzer for Cool, using the Lex/Flex tool.

To be honest, this has bee the most challenging part of the course, since there's so much that I don't understand yet. 

The information I need in order to make this analyzer is so divided into a lot of PDFs and links that I feel that I need a place to jot down all the relevant information about it in one single place, pretty like an API documentation.

So, let's get to work.

# On Cool
## general specification
- Cool programs are sets of *classes*.
- Instances of a class are *objects*
- A class encapsulates variables and procedures of a data type.
    - Classes and types are identified; i.e., every class defines a type.
- Classes permi programmers to define new types and associate procedures (or *methods*) specific to those types.
- Inheritance allows new types to extend the behavior of existing types.

- Cool is an *expression* language.
    - Most Cool constructs are expressions.
    - Every expression has a value and type.

## compiling and running
- reading and running example programs in cool should help
- cool source files have extension `.cl`
    - cool assembly files have extension `.s`
- **example programs** are in the ` /usr/class/cs143/examples` directory.
- **cool compiler** is in the `/usr/class/cs143/bin/coolc` directory
- to compile a program: `coolc [ -o fileout ] file1.cl file2.cl ... filen.cl`
- files are compiled as if ther were concatenated together.
- each file must define a set of complete classes
    - class definitions may not be split across files
- `-o` option specifies an optional name to use for the output assembly code.
    - if the name is not supplied, assembly output is named `file1.s` by default.

- `coolc` compiler generates MIPS assembly code.
- cool programs are run on `spim` MIPS simulator.
- to run a cool program, use:
```s
% spim
(spim) load "file.s"
(spim) run
```
- **To run a different program in the same spin session**, **it's necessary to reinitialize** the state of the simulator before loading the new assembly file
    - You do this by typing `(spim) reinit`
- An (faster) alternative for invoking `spim` with a file is `spim -file file.s`
    - this loads the file, runs the program and then exits `spim`
- Be sure to use `spim` installed on `/usr/class/cs143/bin/spim`

## classes
- Each class definition must be contained in a single source file
- Multiple classes may be defined in the same file
- class definitions have the form:
```
class <type> [ inherits <type> ] {
<feature_list>
};
```
- The notation `[...]` denotes an optional construct.
- All classes names are globally visible
- Class names begin with an uppercase letter.
- Classes may not be redefined.
    - ***Was ist das?***

### features
- the body of the class consists of features
- a feature is either an **attribute** or a **method**.
- an attribute is a variable that will be present on the object of this class.
- a method is a procedure that may manipulate variables and objects of this class.

#### on scope
- all attributes have local scope to the class
- all methods have global scope

#### on naming
- feature's names must start with a lowercase letter.
- no method or attribute name may be defined multiple times in a class
- a method and an attribute can have the same name.

### inheritance
- inheritance syntax: `class C inherits P { ... };`, where **C is the child class** and **P is the parent class**.
- **C** will have all features defined in **P**, plus it's own features.
- if the child and the parent class have a method with the same name, the definition of the child takes precedence.
- it is illegal to redefine attribute names.

#### on inheritance typing (conformance)
- if a variable expects a value of type `P`, then any value of type `C` can be used instead.
- when this happens, we say that `C` *conforms* to `P`.
    - or that `C <= P`, since `C` is lower in the inheritance tree.
- conformance is defined in terms of the inheritance graph.
    - Let `A`, `C` and `P` be types.
    - `A <= A` for all types `A`
    - if `C` inherits from `P`, then `C <= P`
    - if `A <= C` and `C <= P`, then `A <= P`
    - Since `Object` is the root of the graph, `A <= Object` for all types `A`

#### on default inheritance
- there is a distinguished class `Object`.
- if a class does not specify a parent class, then the class inherits from `Object` by default.
- A class may inherit only from a single class
    - this is called **Single Inheritance**
- the parent-child relation on classes defines a graph.
    - this graph may not contain cycles
    - e.g. If **C** inherits from **P**, then **P** must not inherit from **C**
- if **C** inherits from **P**, then **P** must have a class definition somewhere in the program
- Since cool has single inheritance, if all restrictions are satisfied, then the inheritance graph froms a tree with `Object` at the root.

### on basic classes
- besides `Object`, cool has four other basic classes: `Int`, `String`, `Bool` and `IO`.

## Types
- every class name is also a type
- there is a special circumstance type called `SELF_TYPE`
- A type declaration syntax is: `x:C`, where `x` is a variable and `C` is a type.
- every variable must have a type declaration
- all attributes must have a type declaration

### SELF_TYPE
- used to refer to the type of the `self` variable
- useful in classes that will be inherited
- `SELF_TYPE` doesn't have a fixed meaning, because it depends on the calss in which it is used



