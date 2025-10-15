Nice regex builder: https://regex101.com/
# Regex cheat sheet

# Regular Expressions Cheat Sheet

## Anchors
| Symbol | Meaning |
|---------|----------|
| `^` | Start of string (or line in multiline mode) |
| `\A` | Start of string |
| `$` | End of string (or line in multiline mode) |
| `\Z` | End of string |
| `\b` | Word boundary |
| `\B` | Not word boundary |
| `\<` | Start of word |
| `\>` | End of word |

---

## Character Classes
| Symbol | Meaning |
|---------|----------|
| `\c` | Control character |
| `\s` | Whitespace |
| `\S` | Non-whitespace |
| `\d` | Digit |
| `\D` | Non-digit |
| `\w` | Word character |
| `\W` | Non-word character |
| `\x` | Hexadecimal digit |
| `\O` | Octal digit |

---

## POSIX Character Classes
| Class | Description |
|--------|-------------|
| `[:upper:]` | Uppercase letters |
| `[:lower:]` | Lowercase letters |
| `[:alpha:]` | All letters |
| `[:alnum:]` | Letters and digits |
| `[:digit:]` | Digits |
| `[:xdigit:]` | Hex digits |
| `[:punct:]` | Punctuation |
| `[:blank:]` | Space and tab |
| `[:space:]` | Whitespace |
| `[:cntrl:]` | Control characters |
| `[:graph:]` | Printable (non-space) |
| `[:print:]` | Printable (incl. space) |
| `[:word:]` | Letters, digits, underscore |

---

## Assertions
| Symbol | Meaning |
|---------|----------|
| `?=` | Lookahead |
| `?!` | Negative lookahead |
| `?<=` | Lookbehind |
| `?<!` or `?!=` | Negative lookbehind |
| `?>` | Once-only subexpression |
| `?(...)` | Conditional (if-then) |
| `?#` | Comment |

---

## Quantifiers
| Symbol | Meaning |
|---------|----------|
| `*` | 0 or more |
| `+` | 1 or more |
| `?` | 0 or 1 |
| `{3}` | Exactly 3 |
| `{3,}` | 3 or more |
| `{3,5}` | Between 3 and 5 |
> Add `?` after a quantifier to make it **ungreedy**.

---

## Escape Sequences
| Symbol | Meaning |
|---------|----------|
| `\` | Escape next character |
| `\Q` | Begin literal sequence |
| `\E` | End literal sequence |
> Escaping treats special characters literally.

---

## Common Metacharacters
```
^ [ . $ { * ( \ + ) | ? < >
```
> Use `\` to escape them.

---

## Special Characters
| Symbol | Meaning |
|---------|----------|
| `\n` | Newline |
| `\r` | Carriage return |
| `\t` | Tab |
| `\v` | Vertical tab |
| `\f` | Form feed |
| `\xxx` | Octal character |
| `\xhh` | Hex character |

---

## Groups and Ranges
| Pattern | Meaning |
|----------|----------|
| `.` | Any character except newline |
| `(a|b)` | a or b |
| `(...)` | Capturing group |
| `(?:...)` | Non-capturing group |
| `[abc]` | a, b, or c |
| `[^abc]` | Not a, b, or c |
| `[a-q]` | a through q |
| `[A-Q]` | A through Q |
| `[0-7]` | 0 through 7 |
| `\x` | Group number x |

> Ranges are inclusive.

---

## Pattern Modifiers
| Modifier | Meaning |
|-----------|----------|
| `g` | Global |
| `i` | Case-insensitive |
| `m` | Multiline |
| `s` | Treat string as single line |
| `x` | Allow comments and whitespace |
| `e` | Evaluate replacement |
| `U` | Ungreedy pattern |
> *Modifiers marked with `*` are PCRE-specific.*

---

## String Replacement
| Symbol | Meaning |
|---------|----------|
| `$n` | nth captured group |
| `$1`, `$2` | Example: capture groups in regex |
| `$`` | Text before match |
| `$'` | Text after match |
| `$+` | Last captured string |
| `$&` | Entire match |
> Some implementations use `\` instead of `$`.

---
