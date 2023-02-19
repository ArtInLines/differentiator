Currently, to add an operation, you need to add logic for said operation in several places. This is because there is no abstraction over mathematical expressions at the moment.

This document shall outline a plan for adding such abstraction.

Following the advice

## Primitives

There are two kinds of primitives:

1. Numbers
2. Symbols

## Means of Combinations

These primitives can be combined using functions. Syntactically, functions can be prefix or infix, but semantically they're all functions.

Later on, the user should be allowed to define functions themselves and manipulate them as needed.

Applied functions always produce expressions. An expression contains of the applied functions and 0 or more arguments for said function.

Each function should have an associated arity, determining how many arguments it accepts. Said arity should be allowed to be (possibly infinite) ranges.

Each function should also have a precedence associated with it. Paranthesized expressions and prefix-notated functions should always have the highest precedence.

Each function should also have rules for evaluation associated with it. These rules can also contain simplifactions.

Each function should also have information associated with it, that says whether it's commutative or (left-/right-)associative. That might be necessary for simplification rules to work reliably.

## Implementation

Functions need properties associated with them. To implement their associated rules, we also need to have procedures associated with them. Classes might be a useful way to implement them. I feel like there might be an even better way though...

Since the syntax and semantics are supposed to get more complicated, it might be useful to implement a better Parser with a full on AST.

### Implementing functions as terms?

#### Tokenizer

Tokenizer could detect numbers, symbols, parantheses, commas and other characters. If symbols are in front of opening parantheses with no other token in between, then the given set of symbols should be interpreted as the name of a prefix function. If any other character (like +) is found, it should be interpreted as an operator (operators should be able to be both infix and prefix).

The tokens produced by the tokenizer should thus be:

-   `Number`
-   `Name` (Collection of letters, underscores and numbers, where the first symbol isn't a number)
-   `Operator` (Collection of special characters (e.g. `**`))
-   `ParanOpen`
-   `ParanClosed`
-   `Comma`

#### Parser

The grammar for parsing (Uppercase names represent the tokens):

```
exprList	=	expr Comma exprList | expr
expr		=	term | expr Operator term
term		=	Number | Name ParanOpen exprList ParanClosed | Name |  ParanOpen expr ParanClosed
```

The above is slightly incorrect, as it parses Operators without checking their precedence or associatity. To adress that, we split the `expr` rule into `n` rules, where `n` is the highest precedence and `1` is the lowest.

Let `alpha` be the rules for expression for operators of precedence `n` and `beta` be the rules for expressions for operators of precedence `n-1`. Then we have:

```
alpha	=	beta  | alpha (Operator with precedence n) beta
beta	=	gamma | beta (Operator with precedence n-1) gamma
```

If an operator is right-associative instead of left-associative, the rules must be changed like so:

```
alpha	=	beta  | beta (Operator with precedence n) alpha
```

##### Precedence

Precedence is only important for infix operators. The following lists all infix operators with their corresponding precedence:

1. Addition, Subtraction
2. Multiplication, Division
3. Exponentiation

##### Arity

The parser should also check for arity. Each prefix function should have associated with it a certain arity. The parser can check if the provided argument-list is allowed under the given function's arity. The parsing should fail if this is not the case.

## User-Defined Functions

Users should be allowed to define their own functions. These functions must be prefix functions and their names must follow the above described rules for names. If the name is taken by a non-user defined function, an error is thrown. The user must then provide a list of rules for evaluating said function. The arity is taken from said rules.

TODO: How should users define their own functions.

## Storing Evaluation-Rules

Rules fo evaluation should be stored in some kind of data structure, that allows easily adding rules later on. This not only enables easier improvements to the software later on, but also is necessary to add support for user-defined function.

The basic idea is to use a dictionary for storing said rules. SetlX allows storing dictionaries as binary relations (which use red-black-trees under the hood). If necessary these could easily be extended to n-ary relations.

Let $R$ be a binary relation and more specifically a "map" (i.e. $\forall (x, y), (x, z) \in R : y = z$). For all relations $(x, y) \in R$, $x$ is the name of an operator or function and $y$ is a list of rules. Each rule contains of a test function, $t$ and an evaluation function, $e$. Both functions take the list of provided operands as an argument (the operands have beforehand already been evaluated recursively). $t$ should output a boolean, which indicates whether the specified rule should be evaluated or not. $e$ is only called, if $t$ returns true. $e$ should result of the evaluation.
