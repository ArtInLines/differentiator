# Differentiator

A simple computer algebra system (for symbolic manipulation of simple mathematic formulas) written in [SetlX](https://randoom.org/Software/SetlX/).

## Quick Start

1. Download [SetlX](https://randoom.org/Software/SetlX/) (follow instructions on the website to properly install it).
2. Download this repo (or clone it)
3. Open the terminal, move into this repo and run:

```
$ setlX
=> load("diff.stlx");
=> evalStr("3 * x * (x^2 + y)");
```

## Operations & Functions

The following is a list of all operators and functions, that are currently implemented and how their syntax is written.

(Note: `a`, `b` are both placeholders for arbitrary expressions. `x` on the other hand is a placeholder for some variable name).

| Operation      | Syntax       |
| -------------- | ------------ |
| Addition       | `a + b`      |
| Subtraction    | `a - b`      |
| Multiplication | `a * b`      |
| Division       | `a / b`      |
| Exponentiation | `a ^ b`      |
| Negation       | `-a`         |
| Sine           | `Sin(a)`     |
| Cosine         | `Cos(a)`     |
| Derivative     | `Diff(a, x)` |

## Variables

You can use varibales in expressions. For example, `diff(x^2, x)` calculates the derivative of $x^2$ by $x$. Using a `where`-clause you can also substitute certain variables with specific values. For example, `diff(x^2, a) where x = 3a + c` will substitute `x` with `3a + c` and calculate the derivative of $(3a + c)^2$ by $a$ (which evaluates to $18a + 6c$).

There are also built-in variables, that can be used for calculations. These include currently only `Pi` and `e`.

## Naming for Variables and Functions

Any name starting with a lower-case letter is assumed to be a single character. Thus `ab` evaluates to two variables (`a` and `b`), which are multiplied together. To use variables or functions with longer names, you will need to capitalize the name (e.g. `Pi` instead of `pi`).
