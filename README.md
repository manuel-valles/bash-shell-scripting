# Bash Shell Scripting

A complete guide to Bash shell scripting.

## 1. Build a Bash Script

The three core components of a bash script are:

- `SheBang line`

  ```bash
  #!/bin/bash
  ```

  The **file** shell command (`$ file <filename>`) will return the file type (_basic_script: Bourne-Again shell script, ASCII text executable_)

- `Bash commands`

  ```bash
  echo "Hello world!"
  ```

- `Exit statement` (**0** = _Success_; **1-255** = _Failure_)

  ```bash
  exit 0
  ```

If the file execution fails, you will need to provide scripts execute permissions to it. Although a generic way would be with `$ chmod +x <filename>`, it is recommended to set up a more secure script permissions where only the user has the full permissions (**r**: _read_, **w**: _write_, **x**: _execute_):

- `$ chmod <octal code> <filename>`
- By default, go with **744** (_-rwxr--r--_) or **754**(_-rwxr-xr--_) for the octal code (http://permissions-calculator.org/)
- Example: `$ chmod 744 basic_script`

You can always check the permissions of a file or directory with:

- `$ ls -l`
- The first character defines if it is a directory (**d** vs **-**), the following three characters declares the _User_ permissions, then the _Group_'s, and finally the _Others_'.
- Example: `drwxr-xr--`

The `PATH` variable tells the shell where to search for `executable` files, and we can add folders to our `PATH` variables by adding an export line at the very bottom of the `~/.profile` file:

- `export PATH="$PATH:/path/to/script_directory`
- Example: `export PATH="$PATH:$HOME/bash_course/scripts`
- **NOTES**:
  - Do not forget to reload the file: `$ source ~/.profile`
  - Remember that the scripts must have execute permissions to run
  - Try to avoid giving your scripts names that may conflict with another command on the system.

## 2. Variables and Shell Expansions

- **Variables** are parameters (entities that stores values) whose values you can manually change.

  - To create a variable in Bash there must be no spaces around the equal sign: `name=value`.
  - To retrieve the value stored in a parameter/variable it is recommended to use the dollar sign and curly braces: `${parameter}`. This process is also known as **parameter expansion**.
  - There are a few parameter expansion tricks that could be really handy such as:

    - `${parameter^}`: converts the first character of the parameter to uppercase
    - `${parameter^^}`: converts all the characters of the parameter to uppercase
    - `${parameter,}`: converts the first character of the parameter to lowercase
    - `${parameter,,}`: converts all the characters of the parameter to lowercase
    - `${#parameter}`: retrieves the number of characters that the variable's value contains
    - `${parameter:offset:length}`: retrieves the characters from the offset value til the provided length, for example:
      - variable: `numbers=0123456789`
      - command: `echo ${numbers:0:7}`
      - result: `0123456`
      - **NOTES**:
        - if the length is not provided, it would consider the full length: `echo ${numbers:3}` -> `3456789`
        - if the `offset` is negative you will need to leave a whitespace before the minus symbol: `echo ${numbers: -3:2}` -> `78`

  - Some common **Shell variables**:

    - `$HOME`: absolute path to the current user's home directory
    - `$PATH`: list of directories that the shell should search for executable files
    - `$USER`: the current user's username
    - `HOSTNAME`: the name of the current machine
    - `HOSTTYPE`: the current machine's CPU architecture
    - `PS1`: the terminal prompt string

- **Command substitution** is a shell feature that allows to grab the output of a command and do stuff with it:

  - Syntax: `$(command)`
  - Example: `time=$(date +%H:%M:%S)`

- **Arithmetic expansion** is used to perform mathematical calculations in your scripts:

  - Syntax: `$((expression))`
  - Example: `$(( (2 + 3) * 4 ))`
  - **NOTE**: This doesn't return decimal numbers. To do so, you can use the `bc` command which syntax is `echo "scale=<scale>; expression" | bc`, e.g. `echo "scale=2; 5/2" | bc` -> `2.5`

- **Tilde expansion** within the shell is useful when writing scripts that need to work across multiple directories:

  - By default, `~` will expands to the current user's home directory
  - `~<any>` will check to see if `<any>` is a valid username, e.g. `~manu`. If found, then `~manu` is converted to the path to that `manu`'s home directory
  - `~+` is the same as `$PWD`, and `~-` is the same as `$OLDPWD`

- **Brace expansion** is a way of automatically generating text according to a certain pattern. There are two types:
  - _string lists_: `{1,2,3,manu,a,b,c}`
  - _range lists_:
    - Standard: `{1..1000}`
    - With a range increment: `{1..1000..3}`
    - With leading zeros: `{001.100}`
  - _more than one brace expansion_ to a single command line, along with `prefixes` and `postfixes`: `month{01..12}/file{01..31}.txt`
