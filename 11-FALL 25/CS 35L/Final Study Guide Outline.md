## Design principles
**INVEST**: independent (self-contained), negotiable (room for design decisions), valuable, estimable (not vague), small (cannot be split), testable (acceptance criteria)

**separation of concerns**: independent parts, address separate & specific purpose, modular decomposition to reduce complexity

**information hiding principle**: module hides internal design decisions, hide implementation of concerns from other modules, low coupling high cohesion; **single-choice principle**: only one module should know set of alternatives

**solid**: concrete rules for OOP, hide details to reduce complexity
**single responsibility principle**: class has single well-defined responsibility, only one reason to change
**open-closed principle**: module open for extension (subclassing, add behavior) closed for modification
**liskov substitution principle**: subclasses substitutable for superclass without breaking correctness/changing pre or post conditions
**interface segregation principle**: client module should not depend on methods it doesn't use (SRP for interface: split up larger interfaces into smaller coherent interfaces)
**dependency inversion principle**: high-level (abstract) modules should not depend on low-level (concrete) modules, both should depend on abstractions

**security principles**
**CIA**: confidentiality, integrity (modifiable only by authorized, consistent data), availability 
**zero trust**: do not trust users/devices, sanitize all inputs
**open design principle**: robust, public security mechanisms rather than security through obscurity
**public scrutiny**: transparency, can look for vulnerabilities (ex. new approach)
**complementary obscurity**: hide implementation details to hide known vulnerabilities (ex. existing commercial system)

**principle of least privilege**: each program/user operates using least privileges necessary, separate components

**external reuse**: keep versions fixed, use popular modules, regularly check for security patches, strive for fewer dependencies

**internal reuse:** identify violated assumptions

**interoperability**: shared interfaces/data formats
**REST API**: POST, GET, PUT, DELETE


## Networking protocols & layers

## Data management



## Programming languages
**C**: performace optimization, memory management, hardware interaction
**Python**: interpreted (no compile time, slower runtime)
## Software practices

## Design patterns


## RegEx
- Literal characters
- Character classes
	- `[abc]` = character class (one of a, b, or c)
	- Meta characters: `.` (any character), `\d` (digit), `\D` (non-digit), `\s` (whitespace), `\S` (non-whitespace), `\w` (word), `\W` (non-word)
- Quantifiers: `?` (0 or 1), `*` (0+), `+` (1+), `{4}` (exactly 4)
- Anchors: `^` (start), `$` (end), `$^` (matches no string)
- Capture groups: `(abc)` = group (`abc`, `abcabc`, etc.), `|` ("or")
- Non-capture groups: `(?:foo|bar)` = matches "foo" or "bar" but doesn't store as a group
- Named capture groups: `(?<name>pattern)`
- Lookaheads/behinds
	- Lookahead: `X(?=Y)` must have Y after, `X(?!Y)` must not have Y after
	- Lookbehind: `(?<=Y)X` must be preceded by Y, `(?<!Y)X` must not be preceded by Y
**Examples**
- password containing 8+ characters (either letter or number)
	- `^[0-9A-Za-z]{8,}$` 
- to validate email address
	- `^[a-zA-Z0-9.-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$`
	- `^[0-9A-Za-z._-]([a-zA-Z0-9.-_]+[a-zA-Z0-9]+)?@[0-9A-Za-z-]+\..[a-z]{2,}$` 
- no numbers
	- `^[^0-9]*$`
- ends in ?
	- `^.*\?$`
- hex numbers
	- `^0|[1-9A-F][0-9A-F]*0?$`
- floats, no leading 0s
	- `^(?<![\.])(?:(-?0(\.[0-9]+)?)4|(-?([1-9][0-9]*)(\.[0-9]+)?))$`


## Clean code principles and refactoring
**meaningful naming**: not misleading, shorter/abbreviated, conventional (class names = nouns, method names = verbs)
**simplified structure**: reduce nesting, guard clauses, chunking/factor out methods
**purposeful documentation**: document purpose of code and non-obvious details
**defensive programming**: pre/post-conditions, assertions

**refactoring**
inheritance ("pull up" shared methods), extract methods

## Git commands
![500](Pasted%20image%2020251207182722.png)
**basic**
`git push` local -> remote
`git fetch` receive changes from remote + `git merge` applies changes (`git pull` fetch+merge)
`git reset --hard` undo changes in WT
`git add -A` stages all changes, even new files
`git add .` stages all changes, except deletions
`git restore --staged` take changes out of staging w/o changing WT (undo of `git add`)
`git commit -a` only commits tracked files (committed before)
`--amend` edit commit afterwards
`git branch new_branch` + `git checkout new_branch` = `git checkout -b new_branch`
`git merge main` merges changes from main into current branch
detached head: pointing to a commit and not branch
**advanced**
`branch~n` is the nth commit before `branch`
`git cherry-pick B` calculates patch for commit B, creates new commit to add patch to current base (can conflict)
`git stash`, `git stash pop`, `git stash list`, `git stash apply <id>`
`git blame <file>` gives commit ID of last when each line was last edited, author, timestamp
`git bisect start c_good && git bisect run test` run binary search for which commit breaks the tests
`git revert` undo commit in history, `git revert B` applies reverse patch of commit B (can conflict, but non-destructive)
`git rebase -i B` linearizes commit history starting from commit B, destructive
`git merge --squash` combines all patches on feature branch into one commit on target branch
**submodules**
`git submodule add <repo-url> <path>` clones `<repo-url>` into `<path>` and starts tracking as a submodule
`git clone --recursive <repo-url>` clones `<repo-url>` and its submodules, checks out selected commit
`git submodule update` reset submodule content to selected commit

## debugging
**fault**: erroneous location in code -(program exe)-> **error**: incorrect state during execution -(reach boundary)->**failure**: observed incorrect behavior

**debugging steps:** (1) reproduce bug (automated reproduction), locate faulty code (logs, diagrams, refactoring, assertions), determine cause (breakpoints), implement and verify fix (document, run tests)

### vscode debugger
**breakpoints:** line (stops at line), conditional (stops when condition is true), functional (stops when function is called)

## diagram syntax
**class diagrams**
abstract class name italicized
attributes (+) public (-) private
*shape <- rectangle inheritance example*
*state diagram hw example*
**associations**
navigable (has reference) employee/boss
non-navigable (does not have reference)
aggregation (owns) car/wheel, lib/book
composition (needs) person/head, house/room

**ERDs**
cardinality
attributes in ovals
entities in rectangles
relationships in diamonds

**component diagrams**
required interface --(o-- provided interface
*client/server example*

**sequence diagrams**
fragments: alt (conditional), loop (for each, as long as condition true), opt (only if conditions true)

## shell commands
`cd ..` (up one lvl), `cd ~` (root)
`ls`: `-l` (long format), `-a` (include hidden), `-R` (recursive)
`mkdir`: `-p` parent dirs as needed
`cp <source> <dest>`: `-r` recursive
`mv <source> <dest>`: `-n` don't overwrite
`rm <file>`: `-r` recursive (dirs)
`less <file>` display content page by page
`cat <file1> <file2>` concat everything to stdout, `-n` line nums
`sed`: `sed 's/apple/orange/g <file>` replaces "apple" with "orange" (`s` subst, `g` global replacement)
`grep` match patterns: `grep "error" log.txt`, `-i` case insensitive, `-r` recursive (dirs), `-v` invert match
`tr`: `tr 'a-z' 'A-Z` lower to upper, `tr -d 'aeiou` del vowels, `tr -s ' '` squeeze repeated spaces, `tr -cd '0-9` delete non-numbers, `-c` complement
`wc <file>`: `-l` lines, `-w` words, `-c` chars
`sort`: `-r` reverse, `-n` numeric, `-u` unique lines only
`find . -type f -iname "*.log" -delete` find in current dir, type=file ending in .log, delete
`chmod`: `+/-/=` add/rm/set, `r` read, `w` write, `x` execcute, `chmod u+x script.h`
`0` stdinn, `1` stdout, `2` stderr

## shell scripts
```sh
for i in 1 2 3 4 5
do
	echo "Loop $i"
done
```
`-eq` numeric comparison, `=`/`==` string comparison
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

```sh
n=2
varname=n # creates a pointer to the varname
echo="${!varname}"
```
`$?` stores return code of previous command, `if [$? -eq 0]` means non errors
`$0` script name, `$1` arg 1, `$*` all args as one string, `$#` number of args

## make syntax
```c
target: prereq_1 prereq_2 ...
	command_1
	command_2
```

```c
app: main.o utils.o
	 gcc main.o utils.o -o app
main.o: main.c
	 gcc -c main.c
```

`$@` target, `$<` first prereq, `$^` all prereqs

`.PHONY` build target always executed, good for `clean`, `test` (that don't create files)

```c
CC = gcc // set compiler variable

.PHONY: all clean

all: app // set default target at the beginning

app: main.o utils.o // links .o into executable
	$(CC) $^ -o $@

%.o: %.c // compiles .c to .o
	$(CC) -c $< -o $@

clean:
	 rm -f *.o app
```

```c
SRCS = src1.c src2.c
OBJS = $(SRCS:.c=.o) // replace .c with .o: src1.o src2.o

myprog: $(OBJS)
	cc $(OBJS) -o myprog
```
`%` matches all substrings, `:` substitution, `&` for any
`wildcard` is a function that searches the filesystem for all matching file names
```python
SRC_DIR = src
OBJ_DIR = obj

SRCS = $(wildcard $(SRC_DIR)/*.c) # expands to all src/*.c, stored in SRCS
OBJS = $(SRCS:$(SRC_DIR)/%.c=$(OBJ_DIR)/%.o) # for each file in SRCS, replace src/%.c with obj/%.o

$(OBJ_DIR)/%.o: $(SRC_DIR)/%.c
	gcc -c $< -o $@
```



## testing
**unit tests**: individual components in isolation, **integration tests**: components working together, **system/end-to-end**: user input to output
**mock object:** verifies indirect outputs from system, **test spy**: forwards indirect outputs to test, **test stub**: simulates DOC behavior (input and output)
`pytest` run all .py files starting/ending with test in dir/subdir

## DB
**ACID**: atomicity (all or nothing), consistency, isolation (transactions finish before taking effect), durability (permanent)
**CAP**: consistency, availability, partition tolerance