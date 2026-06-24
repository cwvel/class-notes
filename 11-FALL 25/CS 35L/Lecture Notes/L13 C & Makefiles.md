# C
## Benefits of C
- **Speed**
	- C compiles directly to machine code (very close to hardware instructions), greater potential to **optimize performance**
- **Memory management**
	- Explicit manipulation of memory
	- Can write highly optimized code to manage resources precisely
- **Hardware interaction**
	- Great for interfacing directly with hardware, used in device drivers and firmware
- Used in:
	- Operating systems
	- Embedded systems
	- Compilers and assemblers
	- Database management systems

## C++ builds on C
### No OOP
- C is purely **procedural**: functions and data are separate
	- No classes, objects, inheritance or polymorphism
	- **Structs** allow you to define data structures
- C++ is object-oriented
	- Encapsulating functions and data into classes
### No function overloading
- Each function must have a unique name
- In C++, functions can have the same name but a different signature
### No pass-by-references
- Parameters must be passed by value or by pointers
- In C++ you can pass in a reference to the original variable in memory (e.g. `int &a`)
### No built-in try/catch blocks
- **Return values** used instead to indicate errors
	- 0 for success, -1 for error

## More benefits of C
### Smaller executable
- C compilers generate **smaller binaries**
	- Important when you have limited memory to work with
- Complete control over **memory allocation**
	- More predictable execution time
### Library Interface
- Almost all programming languages support calling C functions and can use C libraries
	- Writing a library in C has the widest possible compatibility

## C
### Memory management
- `void *malloc(size_t size)` allocates memory of a given size on the heap
- `void free(void *ptr)` deallocates memory
	- Must free memory to avoid a memory leak
	- Accessing memory that is not allowed by the program results in **segfault**
```c
int* matrix1 = (int*)malloc(rows * cols * sizeof(int));
// ...
free(matrix1);
```

### Reading a file
- `fopen` opens a file
- `fread` reads given amount of data from file stream
- `fclose` closes the file
- These are all *library calls*
```c
FILE *file;
int buffer[5];

// open binary file for reading
file = fopen("input.bin", "rb");
if (file == NULL) {
	perror("Error opening file");
	return 1;
}

// read integers from file into buffer
fread(buffer, sizeof(int), 5, file);

for (int i=0; i<5; i++) {
	printf("Element %d: %d\n", i+1, buffer[i]);
}

// close the file
fclose(file);
return 0;
```

- When creating an executable, the **linker** selects the **libc** implementation for your target operating system

## Creating an executable from source code
- **Compiler/assembler** translates source code into assembly code (**object file**)
- **Linker** resolves *referenced symbols* (function names, global variables)
	- Copies code sections from object files that define those symbols into the exe (**static linking**) or defers until program execution (**dynamic linking**)


`your_file.c` $\xrightarrow{\text{Compiler}}$ `your_file.o` $\xrightarrow{\text{Linker}}$ executable

## C language elements
### Characters and strings
- `'a'` is a single character
- `"a"` is a string (`char*` or `char[]`)
	- Must `#include <string.h>`
	- `'\0'` is not a character, but the character with ASCII value zero marking **end of string**
- Use `const` to indicate that the variable should not be changed
	- ex. `const char*` prevents you from writing into the memory of the pointer
	- Can be cast away, but don't do this

### `goto` allows you to jump to a dfiferent labeled  code locaiton
- Labels with names for code blocks that are only reachable by goto statements
- Don't use!

# Make & Makefiles
## GNU Make
- Incremental build automation
- Useful for large programs
- GNU Make automates building, installing, uninstalling, and testing packages
- Language-independent
- Figures out which files need to be updated based on which source files have changed
	- Only need to re-build parts that have changed

## Anatomy of a makefile
```c
target: prereq_1 prereq_2 ...
	command_1
	command_2
	
mysrc.o: mysrc.c
	cc mysrc.c -o mysrc.o
```
- **Build target**: the **file** you want to produce or a **task** you want to perform
- **Prerequisites**: List of build targets needed to be made before this build target, and files used to make the target
	- All dependencies are made before the build target (only if they have been modified after the build target)
- **Command**: sequence of **shell commands** to build the target/perform the task
	- `cc` compiles a C file into an object file
	- `-c` compiles only, doesn't link
	- `-o` for the object file or executable name

### .PHONY
- Specifies a build target that will **always be executed**
	- Don't check if the files are new and need to be remade
- Commonly used for `clean`, `test`

- ensures that the target will always be excuted when requested, regardless of whether a file with the same name as the target exists in the directory
```c
CC = gcc

default: testOut
testOut: test.o
	$(CC) -o $@ test.o
	
clean:
	rm -f test.o testOut

// in case I have a file named "clean"
.PHONY: clean

```

### Variables
- Variables defined with a string that substitutes the variable name latere
	- `VARNAME = definition`
	- `$(VARNAME)` = definition
- Supports string-replace in variables:
	- `$(VAR:search_pattern=replacement)`
```c
SRCS = src1.c src2.c
OBJS = $(SRCS: .c=.o) # replaces .c with .o

myprog: $(OBJS)
	cc $(OBJS) -o myprog
	
	# translates to: cc src1.o src2.o -o myprog
```

### Pattern rules
- `%` is a **wildcard** that matches any non-empty substring
- `$@` = the target (`testOut`)
- `$^` = all dependencies
- `$<` = first dependencies

```c
%.o: %.c
	cc $< -o $@
```
With the earlier example this translates to: `cc src1.c -o src1.o`
- Makes all object files with the prerequisite of the `.c` source files

```c
test.o: test.c test.h
	$(CC) $(CFLAGS) -c test.c -o test.o
	
test.o: test.c test.h
	$(CC) $(CFLAGS) -c $^ -o $@
	
test.o: test.c test.h
	$(CC) $(CFLAGS) -c $< -o $@
```
*the first and third are syntactically equivalent, the second and the third are functionally equivalent*

#### Wildcards
```
SRC_DIR = src
OBJ_DIR = obj

SRCS = $(wildcard $(SRC_DIR)/*.c)
OBJS = $(SRCS:$(SRC_DIR)/&.c=$(OBOJ_DIR)/&.o)

$(OBJ_DIR)/%.o: $(SRC_DIR)/%.c
	gcc -c $< -o $@
```
- ex. we have many `.c` files in our project in `src/`, and we want to generate object files in `obj/`
- using wildcard
	- `:` = substitution
	- `&` = for any

### Refactoring makefiles
- Variables can be used to reduce duplication
	- Can replace the program name so it can be changed easily
	- Can replace the compiler (gcc, clang)
	- Can summarize compiler flags

- can define constants:
```c
CC = gcc
testOut: test.o
	$(CC) -o testOut test.o
	
[instead of]:
	gcc -o testOut test.o
```
- make will automatically generate the `.o` files for us, so we don't need to create `test.o`, for example