A login shell is the first shell that starts when you sign into a system — it's meant to set up your environment (PATH, env vars,
etc.) for your entire session.

A non-login shell is any shell started after that — like opening a new terminal tab. It assumes the environment is already set up.

- `.bash_profile` / `.zsh_profile` — once, at login. Used by login shells.                                                                                      
- `.bashrc` / `.zshrc` — every new terminal window/tab. Used by non-login shells.
 
- `.bash_profile` is to Bash what `.zsh_profile` is to Zsh. Similarly, `.bashrc` is to Bash what `.zshrc` is to Zsh.

- Since macOS treats each new terminal window as a login shell, `.bash_profile` runs every time. So on Mac, `.bash_profile` and `.bashrc` effectively behave the same way, which is why Mac Bash users just put everything in `.bash_profile`.


# zshrc

zhrc should hold things like

It runs every time you open a new terminal and is where you define things like:

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


## Advanced Topics

- Variables, conditionals, loops in bash        
- Writing and running .sh scripts
- Exit codes and error handling     
- Common utilities like awk, sed, cut, xargs
- Piping and redirection (|, >, >>, 2>&1)                                                                   
That would move you from "understands the shell" to "can automate things with it."