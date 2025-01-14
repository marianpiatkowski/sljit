# SLJIT - Stack Less JIT Compiler

## Purpose:
  A simple, machine independent JIT compiler, which suitable for
  translating interpreted byte code to machine code. The sljitLir.h
  describes the LIR (low-level intermediate representation) of SLJIT.

## Compatible:
  Any C (C++) compiler. At least I hope so.

## Using sljit:
  Copy the content of `sljit_src` directory into your project source directory.
  Add `sljitLir.c` source file to your build environment. All other files are
  included by `sljitLir.c` (if required). Define the machine by `SLJIT_CONFIG_*`
  selector. See `sljitConfig.h` for all possible values. For C++ compilers,
  rename `sljitLir.c` to `sljitLir.cpp`.

  Alternatively, CMake can be used to be tests and the examples in the documentation:

## More info:
  https://zherczeg.github.io/sljit/

## Contact:
  hzmester@freemail.hu

## Special thanks:
  Alexander Nasonov
  Carlo Marcelo Arenas Belón
  Christian Persch
  Daniel Richard G.
  Giuseppe D'Angelo
  H.J. Lu
  James Cowgill
  Jason Hood
  Jiong Wang (TileGX support)
  Marc Mutz
  Martin Storsjö
  Michael McConville
  Walter Lee
  Wen Xichang
  YunQiang Su
