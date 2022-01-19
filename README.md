# Bash Shell Scripting

A complete guide to Bash shell scripting.

## 0. Build a Bash Script

The three core components of a bash script are:

- `SheBang line`

  ```bash
  #!/bin/bash
  ```

  The **file** shell command (`$ file FILENAME`) will return the file type (_basic_script: Bourne-Again shell script, ASCII text executable_)

- `Bash commands`

  ```bash
  echo "Hello world!"
  ```

- `Exit statement` (**0** = _Success_; **1-255** = _Failure_)

  ```bash
  exit 0
  ```

If the file execution fails, you will need to provide scripts execute permissions to it with: `$ chmod +x FILENAME`
