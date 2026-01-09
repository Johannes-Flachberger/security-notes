---
tags:
  - "#type/"
Link: https://www.mingw-w64.org/
Purpose: multi platform cross compiler for windows applications
---
# Info

# Usage

E.g: `i686-w64-mingw32-gcc <source_file> -o <out_file>

The command to use depends on the target architecture:

| Architecture | Command                  |
| ------------ | ------------------------ |
| x86 64 bit   | `x86_64-w64-mingw32-gcc` |
| 32 bit       | `i686-w64-mingw32-gcc`   |

Arguments:

| Argument   | Purpose          |
| ---------- | ---------------- |
| `-l`       | link a library   |
| `-o`       | output file path |
| `--shared` | builld a DLL     |

# Snippets

Compile a dll:

`x86_64-w64-mingw32-gcc windows_dll.c --shared -o output.dll`
