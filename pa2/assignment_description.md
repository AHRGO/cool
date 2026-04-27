# Programming Assignment I

## 1 Overview of the Programming Project
Programming assignments I–IV will direct you to design and build a compiler for Cool. Each assignment will cover one component of the compiler: lexical analysis, parsing, semantic analysis, and code generation. Each assignment will ultimately result in a working compiler phase which can interface with other phases. You will have an option of doing your projects in C++ or Java.

For this assignment, you are to write a lexical analyzer, also called a scanner, using a lexical analyzer generator. (The C++ tool is called flex; the Java tool is called jlex.) You will describe the set of tokens for Cool in an appropriate input format, and the analyzer generator will generate the actual code (C++ or Java) for recognizing tokens in Cool programs.

On-line documentation for all the tools needed for the project will be made available on the ”Project Resources” page of the wiki on the Coursera web site. This includes manuals for flex and jlex (used in this assignment), the documentation for bison and java cup (used in the next assignment), as well as the manual for the spim simulator.

You must work individually on this assignment (no collaboration in groups).

## 2 Introduction to Flex/JLex
Flex allows you to implement a lexical analyzer by writing rules that match on user-defined regular expressions and performing a specified action for each matched pattern. Flex compiles your rule file (e.g., “lexer.l”) to C (or, if you are using JLex, Java) source code implementing a finite automaton recognizing the regular expressions that you specify in your rule file. Fortunately, it is not necessary to understand or even look at the automatically generated (and often very messy) file implementing your rules.

Rule files in flex are structured as follows:
```
%{
Declarations
%}
Definitions
%%
Rules
%%
User subroutines
```

The Declarations and User subroutines sections are optional and allow you to write declarations and helper functions in C (or for JLex, Java). The Definitions section is also optional, but often very useful as definitions allow you to give names to regular expressions. For example, the definition

    \DIGIT [0-9]

allows you to define a digit. Here, `DIGIT` is the name given to the regular expression matching any single character between 0 and 9. The following table gives an overview of the common regular expressions that can be specified in Flex:

| | |
|-|-|
| `x` | the character ”x” |
| `"x"` | an ”x”, even if x is an operator. |
| `\x` | an ”x”, even if x is an operator. |
| `[xy]` | the character x or y. |
| `[x-z]` | the characters x, y or z. |
| `[^x]` | any character but x. |
| `.` | any character but newline. |
| `^x` | an x at the beginning of a line. |
| `<y>x` | an x when Lex is in start condition y. |
| `x$` | an x at the end of a line. |
| `x?` | an optional x. |
| `x*` | 0,1,2, ... instances of x. |
| `x+` | 1,2,3, ... instances of x. |
| `x\|y` | an x or a y. |
| `(x)` | an x. |
| `x/y` | an x but only if followed by y. |
| `{xx}` | the translation of xx from the definitions section. |
| `x{m,n}` | m through n occurrences of x |

The most important part of your lexical analyzer is the rules section. A rule in Flex specifies an action to perform if the input matches the regular expression or definition at the beginning of the rule. The action to perform is specified by writing regular C (or Java) source code. For example, assuming that a digit represents a token in our language (note that this is not the case in Cool), the rule:

    {DIGIT} {
        cool_yylval.symbol = inttable.add_string(yytext);
        return DIGIT_TOKEN;
    }

records the value of the digit in the global variable `cool_yylval` and returns the appropriate token code. (See Sections 5 and 6 for a more detailed discussion of the global variable `cool_yylval` and see Section 4.2 for a discussion of the `inttable` used in the above code fragment.)

An important point to remember is that if the current input (i.e., the result of the function call to `yylex()`) matches multiple rules, Flex picks the rule that matches the largest number of characters. For instance, if you define the following two rules

    [0-9]+ { // action 1}
    [0-9a-z]+ {// action 2}

and if the character sequence 2a appears next in the file being scanned, then action 2 will be performed since the second rule matches more characters than the first rule. If multiple rules match the same number of characters, then the rule appearing first in the file is chosen.

When writing rules in Flex, it may be necessary to perform different actions depending on previously encountered tokens. For example, when processing a closing comment token, you might be interested in knowing whether an opening comment was previously encountered. One obvious way to track state is to declare global variables in your declaration section, which are set to true when certain tokens of interest are encountered. Flex also provides syntactic sugar for achieving similar functionality by using
state declarations such as:

    %Start COMMENT

which can be set to true by writing `BEGIN(COMMENT)`. To perform an action only if an opening comment was previously encountered, you can predicate your rule on `COMMENT` using the syntax:

    <COMMENT> {
        // the rest of your rule ...
    }

There is also a special default state called INITIAL which is active unless you explicitly indicate the beginning of a new state. You might find this syntax useful for various aspects of this assignment, such as error reporting. We strongly encourage you to read the documentation on Lex written by Lesk and Schmidt linked from the Project Resources section on the class wiki before writing your own lexical analyzer.

## 3 Files and Directories
To get started, create a directory where you want to do the assignment and execute one of the following
commands *in that directory*. For the C++ version of the assignment, you should type

    make -f /usr/class/cs143/assignments/PA2/Makefile

Note that even though this is the first programming assignment, the directory name is PA2. Future assignments will also have directories that are one more than the assignment number–please don’t get confused! This situation arises because we are skipping the usual first assignment in this offering of the course. For Java, type:

    make -f /usr/class/cs143/assignments/PA2J/Makefile


## 4 Scanner Results

### 4.1 Error Handling

### 4.2 String Table

### 4.3 Strings

### 4.4 Other Notes

## 5 Notes for the C++ Version of the Assignment

## 6 Notes for the Java Version of the Assignment

## 7 Testing the Scanner

## 8 What to Turn In