# Overview

A login shell is the first shell that starts when you sign into a system — it's meant to set up your environment (PATH, env vars, etc.) for your entire session.

A non-login shell is any shell started after that — like opening a new terminal tab. It assumes the environment is already set up.

- `.bash_profile` / `.zprofile` — once, at login. Used by login shells.

- `.bashrc` / `.zshrc` — every new terminal window/tab. Used by non-login shells.
 
- `.bash_profile` is to Bash what `.zprofile` is to Zsh. 
- Similarly, `.bashrc` is to Bash what `.zshrc` is to Zsh.


# Mac

Since macOS treats each new terminal window as a login shell, `.bash_profile` runs every time. So on Mac, `.bash_profile` and `.bashrc` effectively behave the same way, which is why Mac Bash users just put everything in `.bash_profile`.                                                     
                                                                                 
# Linux

The login shell only reads `.bash_profile`, so anything in `.bashrc` is ignored unless you explicitly source it.

On Linux, `.bash_profile` often sources `.bashrc` to avoid duplication:

  // inside .bash_profile
  if [ -f ~/.bashrc ]; then
      source ~/.bashrc
  fi

This way you only maintain one file (`.bashrc`) and login shells still pick it up. Common pattern worth knowing if you ever work on Linux servers.

# Zsh

macOS terminal apps (Terminal, iTerm2) open non-login shells for Zsh by default, meaning `.zshrc` is always ran.

`.zprofile`, is used only for login shells, i.e SSH sessions, or if you explicitly start a login shell with `zsh -l` or `zsh --login`.

When `.zprofile` Runs:

- Login Sessions: When you first log in to your machine or a remote system via SSH.
- Before .zshrc: It runs before .zshrc, making it suitable for defining variables that .zshrc might need.
   
On a login shell, Zsh loads `.zprofile` first, then `.zshrc` after. So both run, in that order. 

# zshrc & bash_profile

It runs every time you open a new terminal and (`.zhrc` and `.bash_profile`) is where you define things like:

  - Aliases (alias gs="git status")
  - Environment variables (export PATH=...)
  - Prompt customization
  - Plugin/tool setup (like oh-my-zsh, nvm, etc.)

##  Environment variables

key/value pairs available to your shell and any programs you run. Common ones:

  - PATH — tells the shell where to look for executables
  - NODE_ENV — tells Node.js which environment you're in (development, production)
  - API_KEY — store secrets/config outside your code

## Prompt customization

Changing what your terminal prompt looks like. By default it might just show `$`, but you can make it show your current directory, git branch, username, colors, etc.


# Advanced Topics

- Variables, conditionals, loops in bash        
- Writing and running .sh scripts
- Exit codes and error handling     
- Common utilities like awk, sed, cut, xargs
- Piping and redirection (|, >, >>, 2>&1)                                                                   

That would move you from "understands the shell" to "can automate things with it."
