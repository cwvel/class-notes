# Shell Scripting
## Shell commands
### Files
- `cd <dir>`
	- `cd ..` up one level
	- `cd ~` home directory
- `ls` 
	- `-l` long format
	- `-a` include hidden files
	- `-R` recursive (for directories containing files, etc.)
- `mkdir
	- `-p` make parent directories as needed
- `cp <source> <dest>`
	- `-r` recursive
- `mv <source> <dest>`
	- `-n` do not overwrite existing files
- `rm <file>`
	- `-r` recursive (deletes directories)
- `less <file>` displays content page by page
- `cat <file> <file>` concatenates everything to stdout (can concatenate multiple files to stdout)
	- `-n` numbers all output lines
### Text processing
- `sed`
	- stream editor: search/find/replace/insert or delete
	- `sed 's/apple/orange/g <file>` replaces all "apple" with "orange" (`s` = substitution, `g` = global replacement)
- `grep` global regular expression print: searches for patterns inside files and prints matches
	- `grep "error" log.txt`
	- `-i` case-insensitive
	- `-r` recursive search in directories
	- `-v` invert match (show lines *not* matching)
- `tr` translate and delete characters
- `head/tail <file>` displays the first/last few lines of a file
	- `-n` specify number of lines
- `wc <file>` word and line count (`-l` = lines, `-w` = words, `-c` = chars)
- `sort` sorts lines of texts `-r` = reverse order, `-n` = numeric order, `-u` sort unique lines only
- `cut` extracts specific columns/fields (`-d` = delimiter, `-f` = field)
### Others
- `ssh <remote>`
- `htop` interactive process viewer: shows all running processes (similar to task manager)
- `man <command>` manual
- `pwd` print working directory
- `chmod` change mode: change the permissions of files/directories
	- `+/-/=` add/remove/set permission
	- `r` = read, `w` = write, `x` = execute
	- `chmod u+x script.sh`
## Input/output
- piping `|` connects stdin/stdout/stderr of different commands
- streams are a sequence of bytes
	- `0` = stdin, `1` = stdout, `2` = stderr
- read from file: `cmd < file`
- write to file: `cmd > file`
	- `2>` redirect stderr to a file
	- `1>` redirect stdout to a file
	- `2>&1` redirects stderr to stdout
	- `>>` append instead of overwrite
## Syntax
### Shebang
- `#!/bin/sh` for simple scripts
- `#!/bin/bash` for complex scripts (bash has arrays, more regex, etc.)
	- bash is a specific implementation of the shell

### Variables
- `read $VAR`
- `echo "hello $USER"`
- `$1` = first argument of command
- Reading an undeclared variable results in an empty string

### For loops
```sh
for i in 1 2 3 4 5
do
	echo "Loop $i"
done
```
### If statements
- `-eq` for equality numeric comparison
- `=` and `==` for string comparison
```sh
m=1
n=1.0

if [$n -eq $m]
then
	echo "Same"
else
	echo "Different"
fi
```

### Pointers
```sh
m=1
n=2
varname=n # creates a pointer to the varname
echo="${!varname}"
```

### Example: Find and delete
`find . -type f -iname "*.log" -delete`
- `.` searches in current directory
- `-type f` only matches regular files (not directories or links)
- `"*.log` only files ending in .log, ignoring case
- `-delete` permanently deletes the files found

### Check exit status
- `$?` stores the return code of the previous command
	- `if [$? -eq 0];` means there are no errors (code: `0`)

### Argument handling
- When you run a script, arguments are passed after the script name:
	- `./script.sh arg1 arg2 arg3`
- Within the script:
	- `$0` = script name
	- `$1` = first argument
	- `$*` = all arguments in a single string
	- `$#` = number of arguments passed

### Exporting variables
```sh
> $MYVAR = hello
> export MYVAR
> ./myvar2.sh
```
- After exporting the variable, it is inherited by the next program. but if this program changes the value of MYVAR it will not be passed back to the interactive shell
	- sourcing the script: allows the change to be passed back to the shell
	- `. ./myvar2.sh`

# W1 Discussion Shell Lab

>[!definition] Useful commands
>ls – show files in current directory
>cd – enter a specific directory (Use “..” to go back)
>rm – remove a file
>cp – copy a file
>mv – move a file
>mkdir – create a directory
>echo – print text to terminal
>man – used to check the documentation of previous commands (“man rm”)

**Implement a Bash script called “remove” that…**
On invocation of “remove A B C”:
- Delete the files/directories A, B, and C
- Save a backup of the deleted files in ~/Trash
- Save the name of the file in ~/trash-history.log

`#!/bin/bash` shebang = specifies which language to use

`set -e` line at the beginning, immediately stops program after encountering an error

`$1` takes the first argument, `$2` for the second, etc. (`./a first second`)
`$@` takes all arguments at once

`mv "$@" ~/Trash`
- quotation marks prevents accidental splitting

If `~/Trash` doesn't exist, create it: `mkdir -p ~/Trash`
- `-p` makes it so that it won't throw an error if it already exists (if not it'll create all the directories leading up to it)

`echo "$@" >>/~trash-history.log`
- `>>` to append to file instead of overwriting it

use a for loop to put each file on a new line:
```sh
for x in "$@" ; do
    echo "$x" >>~/trash-history.log
done
```

check for no arguments:
```sh
if [ -z "$1 ]; then
    echo "Please provide a file!"
    exit 1
fi
```

final script;
```sh
#!/bin/bash

set -e

if [-z "$1]; then
    echo "Please provide a file!"
    exit 1
fi

mkdir -p ~/Trash

mv "$@" ~/Trash

for x in "$@"; do
    echo "$x" >>~/trash-history.log
done

```

