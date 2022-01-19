# Bash Shell Scripting

A complete guide to Bash shell scripting.

## 0. Build a Bash Script

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
- Do not forget to reload the file: `$ source ~/.profile`
- _NOTE_: Remember that the scripts must have execute permissions to run!
- **IMPORTANT**: Try to avoid giving your scripts names that may conflict with another command on the system.
