# FunCompiler

FunCompiler is a statically typed, functional programming language which is a subset of C. Whitespace is ignored and there are no required expression delimiters. That's right: no semi-colons and no forced indent!

## Dependencies

- [CMake >= 3.14](https://cmake.org/)
- Any C Compiler (We like [GCC](https://gcc.gnu.org/))

## Build

1. generate a build tree using CMake.
```shell
  cmake -B bld
```

2. build an executable from the build tree.
```shell
  cmake --build bld
```

*** To build generated x86_64 ASM

GNU Binutils:
```shell
  as code.S -o code.o
  ld code.o -o code
```

GNU Compiler Collection
```shell
  gcc code.S -o code.exe
```

LLVM/Clang
```shell
  clang code.S -o code.exe --target=x86_64
```

To use external calls, link with appropriate libraries!

## Language Reference

The language is statically typed.
Variables must be declared and type annotated before use.

Whitespace is ignored and there are no required expression delimiters.
That's right: no semi-colons and no forced indent!

Functions are first-class citizens.

A program in this language comes in the form of a file. The file may
contain a series of expressions that will be executed in order, from
top to bottom. There is no =main= function or other entry point;
control flow starts at the very top of the file and makes it's way to
the bottom of the file.

Let's take a look at a basic program:
```fun
fact : integer (n : integer) = integer (n : integer) {
  if n < 2 {
    1
  } else {
    n * fact(n - 1)
  }
}

fact(5)
```

This program will return 120 as a status code. The result of the last
expression in the file is the return value. The same holds true for
function bodies, and if/else bodies.

Variables in a local scope shadow variables in a parent scope, and may
share the same symbolic name.
