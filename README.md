# pacli-environment
This utitility let you working in the "pacli enviroment", i.e. basically you don't have to type "pacli" before any pacli command.

## Dependencies

- `pacli` installed at **`/bin/pacli`** or **`~/.local/bin/pacli`**
- **rlwrap** (line editing, history, completion)  
  - Debian/Ubuntu: `sudo apt install rlwrap`  
  - macOS (Homebrew): `brew install rlwrap`  
  - Arch: `sudo pacman -S rlwrap`

> **Note:** Start/stop **slimcoind** yourself in a separate terminal. This shell does **not** manage the daemon.

## Files in this folder

- `pacli_env` – launcher that wraps `pre_pacli_env` with `rlwrap`
- `pre_pacli_env` – the interactive shell (Bash)
- `pacli_words` – example word list for completion (you can copy to `~/.pacli_words`)

## Installation

```bash
# Put the files into a folder, then:
chmod 755 pacli_env pre_pacli_env

# Optional: install the word list for rlwrap
cp pacli_words ~/.pacli_words
```

(Optional) make the launcher available system-wide:

```bash
sudo ln -s "$(pwd)/pacli_env" /usr/local/bin/pacli_env
# or:
sudo ln -s "$(pwd)/pacli_env" /bin/pacli_env
```

## Usage

```bash
# Terminal 1: start your daemon as usual
slimcoind ...

# Terminal 2: start the pacli shell
pacli_env
```

Examples inside the shell:

```
pacli > deck list
pacli > card send ...
pacli > card list | grep foo
pacli > card list > out.txt
pacli > exit
```

## Completion word list

`rlwrap` can complete from a simple word file. Minimal example:

```
# ~/.pacli_words  (one word per line)
deck
card
address
swap
help
quit
```

Extend this file with your most used commands/keywords.

## Security note

`pre_pacli_env` uses **`eval`** to preserve shell-style quoting. This makes shell metacharacters such as `|`, `>`, `;`, `&&`, `$()`, backticks, etc. active.  
Convenient for testing (`| grep`, redirections), but **do not paste untrusted input** and **do not run as root**.

---
