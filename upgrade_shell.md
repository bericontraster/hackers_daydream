# Shell Upgrade

This doc contain all the commands you can use to upgrade your reverse shells :]

# ` Python `
```python3
  python3 -c 'import pty; pty.spawn("/bin/bash")'
```
## **How does this command works?**  
This command launches a pseudo-terminal shell in the current terminal session using the Python programming language.

More specifically, the command imports the **pty** module in Python which provides functionality for controlling pseudo-terminals. It then calls the **spawn()** function from the pty module to start a new interactive shell process **(/bin/bash)** with the current terminal as its controlling terminal. This effectively gives you a fully interactive shell with access to all the features of a normal shell.

This can be useful in situations where you are connected to a remote system via SSH or some other protocol and want to gain a more fully-featured shell session with things like tab completion, job control, and so on. The pty module provides a way to create a fully interactive shell session even if the remote system doesn't support it natively.


# `Typescript`
```sh
script /dev/null/ -c bash
```
## **How does this command works?**  
The command script **/dev/null/ -c bash** starts a new shell session and logs all input and output to a file named typescript in the current directory.

The script command is used to make a typescript or record of a terminal session. **/dev/null/** is a special file that discards all data written to it, so in this case, it is being used to discard the typescript output.

The **-c** option tells script to execute a command and then exit. In this case, the command being executed is bash, which starts a new shell session.

So, when you run this command, it starts a new shell session and records all input and output to a file named typescript in the current directory. However, since the output is being discarded to /dev/null/, the typescript file will be empty.  

