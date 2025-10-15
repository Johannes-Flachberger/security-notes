**Type:** #type/tool
**Tags:**  
**Link:**  https://www.vim.org/
**Purpose:** best commandline editor ever

---
# Info

# Usage
show line number: `:set nu`
# 🧠 Vim Cheat Sheet

## 📍 Moving
| Command | Description |
|----------|--------------|
| `h` | Move left |
| `j` | Move down |
| `k` | Move up |
| `l` | Move right |
| `#h [j/k/l]` | Move multiple times in direction |
| `b / B` | Move to start of word / WORD |
| `w / W` | Move to next word / WORD |
| `e / E` | Move to end of word / WORD |
| `0` | Jump to start of line |
| `$` | Jump to end of line |
| `^` | Jump to first non-blank character |
| `#G / #gg / :#` | Go to specific line |

---

## 🧩 Moving by Screens
| Command | Description |
|----------|--------------|
| `Ctrl+b` | Move back one full screen |
| `Ctrl+f` | Move forward one full screen |
| `Ctrl+d` | Move forward half a screen |
| `Ctrl+u` | Move back half a screen |
| `Ctrl+e` | Scroll screen down one line |
| `Ctrl+y` | Scroll screen up one line |
| `H` | Move to top of screen |
| `M` | Move to middle of screen |
| `L` | Move to bottom of screen |

---

## ✍️ Inserting
| Command | Description |
|----------|--------------|
| `i` | Insert before cursor |
| `I` | Insert at beginning of line |
| `a` | Insert after cursor |
| `A` | Insert at end of line |
| `o` | Open new line below |
| `O` | Open new line above |
| `ea` | Insert at end of word |
| `Esc` | Exit insert mode |

---

## ✂️ Editing
| Command | Description |
|----------|--------------|
| `r` | Replace one character |
| `cc` | Replace entire line |
| `C / c$` | Replace to end of line |
| `cw` | Replace word |
| `s` | Delete character and insert |
| `J` | Join line below with space |
| `gJ` | Join line below without space |
| `.` | Repeat last command |

---

## ↩️ Undo / Redo
| Command | Description |
|----------|--------------|
| `u / :u / :undo` | Undo last change |
| `#u` | Undo multiple changes |
| `U` | Undo all changes on line |
| `Ctrl+r` | Redo last undone change |
| `:undolist` | Show undo branches |

---

## 🧮 Copying (Yanking)
| Command | Description |
|----------|--------------|
| `yy` | Copy line |
| `#yy` | Copy multiple lines |
| `yaw` | Copy word (with space) |
| `yiw` | Copy word (without space) |
| `y$` | Copy right of cursor |
| `y^` | Copy left of cursor |
| `ytx` | Copy until character x |
| `yfx` | Copy including character x |

---

## ✂️ Cutting (Deleting)
| Command | Description |
|----------|--------------|
| `dd` | Cut current line |
| `#dd` | Cut multiple lines |
| `d$` | Cut to end of line |
| `dw` | Cut word |
| `:#,#d` | Cut range of lines |
| `:%d` | Cut all lines |
| `dgg` | Cut to start of file |
| `:.,$d` | Cut to end of file |
| `:g/pattern/d` | Cut matching lines |
| `:g!/pattern/d` | Cut non-matching lines |
| `:g/^$/d` | Cut blank lines |

---

## 📋 Pasting
| Command | Description |
|----------|--------------|
| `p` | Paste after cursor |
| `P` | Paste before cursor |

---

## 🔠 Visual Mode
| Command | Description |
|----------|--------------|
| `v` | Visual (character) mode |
| `V` | Visual (line) mode |
| `Ctrl+v` | Visual block mode |
| `o` | Switch selection end |
| `aw` | Select word |
| `ab / aB / at` | Select block (), {}, <> |
| `ib / iB / it` | Inner block (), {}, <> |

---

## 🏷️ Marks and Jumps
| Command | Description |
|----------|--------------|
| `m[a-z]` | Set mark |
| `'a` / ``a`` | Jump to mark |
| `:marks` | List marks |
| `:jumps` | List jumps |
| `:changes` | List changes |
| `Ctrl+i / Ctrl+o` | Move forward/backward in jump list |
| `g, / g;` | Move in change list |

---

## 📂 Multiple Files & Windows
| Command | Description |
|----------|--------------|
| `:e file` | Open file |
| `:bn / :bp` | Next / previous buffer |
| `:bd` | Close buffer |
| `:ls` | List buffers |
| `:sp file` | Split horizontally |
| `:vs file` | Split vertically |
| `gt / gT` | Next / previous tab |
| `Ctrl+ws / Ctrl+wv` | Split screen horizontally / vertically |
| `Ctrl+ww` | Switch between splits |
| `Ctrl+wq` | Quit split |
| `Ctrl+wx` | Exchange splits |
| `Ctrl+=` | Equalize split sizes |

---

## 🔍 Searching
| Command | Description |
|----------|--------------|
| `/pattern` | Search forward |
| `?pattern` | Search backward |
| `n` | Repeat search same direction |
| `N` | Repeat search opposite direction |
| `*` | Search next word under cursor |
| `#` | Search previous word under cursor |

---

## ⚙️ Macros
| Command | Description |
|----------|--------------|
| `qa` | Record macro into register a |
| `q` | Stop recording |
| `@a` | Execute macro a |
| `@@` | Repeat last macro |

---

## 🎨 Color Schemes
| Command | Description |
|----------|--------------|
| `:colorscheme [name]` | Apply color scheme |
| `:colorscheme [space]+Ctrl+d` | List available schemes |


