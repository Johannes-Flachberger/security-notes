---
tags:
  - "#type/tool"
  - "#attack/ressource-development"
Link:
Purpose: compiler framework for linux
---
# Info

# Usage

## Compiling for the same architecture

Example: `gcc exploit.c -o exploit -static`

Note: `-static` links all libraries statically, this way the exploit might even work if the target has other library versions installed

## Compiling for 32 bit targets

Example: `gcc -m32 exploit.c -o exploit -static`

## Cross-Compiling on Linux Arm for x64

 `x86_64-linux-gnu-gcc <source> -o <outfile>`

> [!Hint] Hint
> For a successful cross-compilation, the glibc version must be older or equal to the targets glibc version.

# Snippets
