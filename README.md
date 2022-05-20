# simple_shell
A simple UNIX command interpreter making as a final project of the low-level programming and algorithm quarter at ALX school of software engineering

# Overview
Lively is a sh-compatible command language interpreter that executes commands read from the standard input or from a file.

# Invocation
Usage: Lively is started with the standard input connected to the terminal. To start, compile all .c located in this repository by using this command:

gcc -Wall -Werror -Wextra -pedantic *.c -o lively ./lively Lively is allowed to be invoked interactively and non-interactively. If lively is invoked with standard input not connected to a terminal, it reads and executes received commands in order.

# Example:
$ echo "echo 'holberton'" | ./lively 'ALX' $ When sodash is invoked with standard input connected to a terminal (determined by isatty(3), the interactive mode is opened. lively Will be using the following prompt ^-^ .

# Example:
$./lively ^-^ If a command line argument is invoked, lively will take that first argument as a file from which to read commands.

# Example:
$ cat text echo 'ALX' $ ./lively text 'ALX' $

# Environment
Upon invocation, lively receives and copies the environment of the parent process in which it was executed. This environment is an array of name-value strings describing variables in the format NAME=VALUE. A few key environmental variables are:

# HOME
The home directory of the current user and the default directory argument for the cd builtin command.

$ echo "echo $HOME" | ./lively /home/vagrant

# PWD
The current working directory as set by the cd command.

$ echo "echo $PWD" | ./lively /home/vagrant/ALX/simple_shell

# OLDPWD
The previous working directory as set by the cd command.

$ echo "echo $OLDPWD" | ./lively /home/vagrant/ALX/bog-062019-test_suite

# PATH
A colon-separated list of directories in which the shell looks for commands. A null directory name in the path (represented by any of two adjacent colons, an initial colon, or a trailing colon) indicates the current directory.

$ echo "echo $PATH" | ./lively /home/vagrant/.cargo/bin:/home/vagrant/.local/bin:/home/vagrant/.rbenv/plugins/ruby-build/bin:/home/vagrant/.rbenv/shims:/home/vagrant/.rbenv/bin:/home/vagrant/.nvm/versions/node/v10.15.3/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/home/vagrant/.cargo/bin:/home/vagrant/workflow:/home/vagrant/.local/bin

# Command Execution
After receiving a command, lively tokenizes it into words using " " as a delimiter. The first word is considered the command and all remaining words are considered arguments to that command. Lively then proceeds with the following actions:

If the first character of the command is neither a slash () nor dot (.), the shell searches for it in the list of shell builtins. If there exists a builtin by that name, the builtin is invoked. If the first character of the command is none of a slash (), dot (.), nor builtin, lively searches each element of the PATH environmental variable for a directory containing an executable file by that name. If the first character of the command is a slash () or dot (.) or either of the above searches was successful, the shell executes the named program with any remaining given arguments in a separate execution environment.

# Exit Status
Lively returns the exit status of the last command executed, with zero indicating success and non-zero indicating failure. If a command is not found, the return status is 127; if a command is found but is not executable, the return status is 126. All builtins return zero on success and one or two on incorrect usage (indicated by a corresponding error message).

# Signals
While running in interactive mode, lively ignores the keyboard input ctrl+c. Alternatively, an input of End-Of-File ctrl+d will exit the program.

User hits ctrl+d in the foutrh command.

$ ./lively ^-^ ^C ^-^ ^C ^-^ ^C ^-^

# Variable Replacement
Lively interprets the $ character for variable replacement.

$ENV_VARIABLE
ENV_VARIABLE is substituted with its value.

Example:

$ echo "echo $PWD" | ./lively /home/vagrant/ALX/simple_shell

# $?
? is substitued with the return value of the last program executed.

Example:

$ echo "echo $?" | ./lively 0 $$ The second $ is substitued with the current process ID.

Example:

$ echo "echo $$" | ./lively 3855

# Comments
Lively ignores all words and characters preceeded by a # character on a line.

Example:

$ echo "echo 'alx' #this will be ignored!" | ./lively 'alx'

# Operators
Lively specially interprets the following operator characters:

; - Command separator Commands separated by a ; are executed sequentially.

Example:

$ echo "echo 'hello' ; echo 'world'" | ./lively 'hello' 'world'

# && - AND logical operator
command1 && command2: command2 is executed if, and only if, command1 returns an exit status of zero.

Example:

$ echo "error! && echo 'ALX'" | ./lively ./shellby: 1: error!: not found $ echo "echo 'my name is' && echo 'ALX'" | ./livey 'my name is' 'ALX'
# || - OR logical operator
command1 || command2: command2 is executed if, and only if, command1 returns a non-zero exit status.

Example:

$ echo "error! || echo 'wait for it'" | ./lively ./lively: 1: error!: not found 'wait for it' The operators && and || have equal precedence, followed by ;.

# Builtin Commands
#  cd
Usage: cd [DIRECTORY] Changes the current directory of the process to DIRECTORY. If no argument is given, the command is interpreted as cd $HOME. If the argument - is given, the command is interpreted as cd $OLDPWD and the pathname of the new working directory is printed to standad output. If the argument, -- is given, the command is interpreted as cd $OLDPWD but the pathname of the new working directory is not printed. The environment variables PWD and OLDPWD are updated after a change of directory. Example:

$ ./lively ^-^ pwd /home/vagrant/ALX/simple_shell $ cd ../ ^-^ pwd /home/vagrant/ALX ^-^ cd - ^-^ pwd /home/vagrant/ALX/simple_shell

# exit
Usage: exit [STATUS] Exits the shell. The STATUS argument is the integer used to exit the shell. If no argument is given, the command is interpreted as exit 0. Example:

$ ./lively $ exit

# env
Usage: env Prints the current environment. Example:

$ ./lively $ env NVM_DIR=/home/vagrant/.nvm ...

# setenv
Usage: setenv [VARIABLE] [VALUE] Initializes a new environment variable, or modifies an existing one. Upon failure, prints a message to stderr. Example:

$ ./lively $ setenv NAME Alx $ echo $NAME Alx

# unsetenv
Usage: unsetenv [VARIABLE] Removes an environmental variable. Upon failure, prints a message to stderr. Example:

$ ./lively $ setenv NAME Holberton $ unsetenv NAME $ echo $NAME



# Authors & Copyright
Fatima Nankor Acheampong
Enoch Enu.


# More information
Lively is a simple shell unix command interpreter that is part of the alx low level programming module at Alx School and is intended to emulate the basics sh shell. All the information given in this README is based on the lively and bash man (1) pages.
