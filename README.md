# clipd: macOS Clipboard History Daemon
Watches your macOS clipboard in the background and saves a history of copied text and files.

---

## Overview
```
Usage: clipd [commands] [id]
       clipd search <query>

Commands:
  watch             Start the background daemon to record clipboard history
  stop              Stop the active clipd daemon
  status            Check if the daemon is running and see history count
  list              Show all items copied to the clipboard (up to 100)
  paste [id]        Paste an item back to clipboard. If no id provided, uses fzf
  search <query>    Search your clipboard history for a keyword
  remove <id>       Delete a specific item from history
  echo <id>         Print a text item directly to stdout (for piping)
  reset             Clear the entire clipboard history
  -h | --help       Show help message

Conventions:
  - LIFO Stack: Latest copied items appear at the top of the list.
  - Strict Deduplication: No duplicate entries are ever saved.

Examples:
  # Start the clipboard daemon in the background
  clipd watch

  # View the clipboard history and their IDs
  clipd list

  # Paste the 3rd item from history back to the clipboard
  clipd paste 3

  # Interactively select an item to paste using fzf
  clipd paste

  # Search history for a specific URL or word
  clipd search "github"

  # Pipe a copied text snippet directly into grep without touching the clipboard
  clipd echo 2 | grep "error"

  # Delete a sensitive item from history
  clipd remove 4

  # Stop the daemon 
  clipd stop

  # Stop the daemon and clear all history
  clipd reset
```
---

## Installation & Setup
1. **Clone the repository and cd into the directory**:
   ```bash
   git clone https://github.com/taraqfarhan/clipd
   cd clipd
   ```

2. **Make the script executable**:
   ```bash
   chmod +x clipd
   ```

3. **Add to PATH**:
   To use the `clipd` command globally, symlink it to a directory in your shell's path (such as `/usr/local/bin`):
   ```bash
   ln -s "$(pwd)/clipd" /usr/local/bin/clipd
   ```

4. **(Recommended) Install `fzf` for interactive mode**:
   If you want to use `clipd paste` without an ID to open an interactive selection menu, install `fzf` via Homebrew:
   ```bash
   brew install fzf
   ```