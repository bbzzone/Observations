# Makefiles

```makefile
TARGETS=leet.c made.c test.c logfind.c
OBJECTS=leet made test logfind

# target: dependencies
#	action

all: $(OBJECTS)

%: %.c
	gcc -o $@ $^
clean:
	rm -If $(OBJECTS)
```

the very 1st rule here is 

1. `all: $(OBJECTS)`. Now $(OBJECTS) will be replaced with placeholders like `leet made test logfind`. So technically this statement is like `all: leet made test logfind`. It means that target `all` needs `leet made test logfind` as dependencies. Than in makefile target `leet made test logfind` will be searched. But here there is no target specifying the same. But % is a wildcard for anything so it will also hold true if we say that target is `leet made test logfind`. 
2. `%: %.c`  is simply specifying `target: dependencies`. So as % is placeholder for anything, it is our target and %.c simply says if our target is `leet` than our dependency will be target suffixed with .c (`target.c`). 
3. `gcc -o $@ $^.`  Here simply we are compiling the files. `$@` is a placeholder for current target and `$^` is placeholder for dependency. 
4. **How this will work:**  Here `all: $(OBJECTS)` will represent `all: leet made test logfind` than all will try to build it's 1st dependency, which is leet. It will search for target *leet* and *%* will cover that So it will run that target like `leet:leet.c` and than **$@ = leet** and **$^ = leet.c**.

We can also create a Makefile like below:

```makefile
CFLAGS=-Wall -Wextra -g -lm

TARGETS=$(wildcard *.c)
OBJECTS=$(patsubst %.c,%,$(TARGETS))

all: $(OBJECTS)

$(OBJECTS): $(TARGETS)
	gcc -o $@ $(patsubst %,%.c,$@)

clean:
	rm -f $(OBJECTS)
```

This is doing the same thing as previous one but here we don't need to specify all the c files explicitly. Use of **wildcard and patsubst** made things easier. In makefile `wildcard *.c` will list all the files ending with .c in the current directory. `patsubst %.c,%,$(TARGETS)` will stripout .c from the values in TARGETS list. 

again all be converted to `all: leet.c made.c logfind.c` and than `$(OBJECTS): $(TARGETS)` will also be substituted with corresponding values. For leet.c it will look like this

```makefile
leet: leet.c
	gcc -o leet $(patsubst leet,leet.c,leet)
```

So leet will be converted to leet.c with the help of `patsubst`. 

```makefile
HEADERS=. ./src

CFLAGS=-Wall -Wextra -g -lm $(foreach D $(HEADERS) I$(D))
# I flag set the dirs to be searched for header files
# I./src will search for header files in src dir
DEPFLAGS=-MP -MD
```

DEPFLAGS are dependency flags. It simply means that if any of dependency (i.e. header files) is changed than compile the whole code again.

**.PHONY:** Any make rule always assume that it's target is a file. For `make leet`. Make will think that leet is a file, So before updating it will check if the file is modified or not. If not it will ignore the make action associated with the *target*. For example if you have a file named "clean" in your directory, when calling `make clean`, make will check if the file is upto date or not if it is not modified than instead of taking action it will simply abort by saying that `clean is upto date`. So to avoid that and ignore clean file so that target can run without any intruptions, one can set *.PHONY=clean*. So whenever clean is called the file named clean is ignored. 

