# Vim Cheatsheet

## Modes
| Key | Action |
|-----|--------|
| `i` | Insert mode (before cursor) |
| `a` | Insert mode (after cursor) |
| `o` | Insert mode (new line below) |
| `O` | Insert mode (new line above) |
| `Esc` | Back to Normal mode |
| `v` | Visual mode (character) |
| `V` | Visual mode (line) |


---

## Navigation
| Key | Action |
|-----|--------|
| `k` | Move up |
| `j` | Move down |
| `h` | Move left |
| `l` | Move right |
| `w` | Next word (start) |
| `b` | Previous word (start) |
| `0` | Start of line |
| `^` | First non-blank character of line |
| `$` | End of line |
| `gg` | Go to first line |
| `G` | Go to last line |
| `Ctrl+d` | Scroll half page down |
| `Ctrl+u` | Scroll half page up |


---

## Editing
| Key | Action |
|-----|--------|
| `x` | Delete character under cursor |
| `dd` | Delete (cut) current line |
| `{n}dd` | Delete n lines (e.g. `3dd`) |
| `dw` | Delete word |
| `d$` | Delete to end of line |
| `cc` | Change (delete + insert) current line |
| `ciw` | Change inner word (replace word under cursor) |
| `cw` | Change word |
| `r{c}` | Replace single character with c |
| `u` | Undo |
| `Ctrl+r` | Redo |
| `yy` | Copy current line |
| `p` | Paste after cursor |
---

## Search
| Key | Action |
|-----|--------|
| `/{pattern}` | Search |
| `n` / `N` | Next / previous match |
| `*` | Search word under cursor |

---

## Save & Quit
| Command | Action |
|---------|--------|
| `:w` | Save |
| `:wq` | Save and quit |
| `:q!` | Quit without saving |
