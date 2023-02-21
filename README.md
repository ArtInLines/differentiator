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

| Operation | Syntax |
| --- | --- |
| Addition | `a + b` |
| Subtraction | `a - b` |
| Multiplication| `a * b` |
| Division | `a / b` |
| Exponentiation | `a ^ b` |
| Negation | `-a` |
| Sine | `sin(a)` |
| Cosine | `cos(a)` |
| Derivative | `diff(a, x)` |
