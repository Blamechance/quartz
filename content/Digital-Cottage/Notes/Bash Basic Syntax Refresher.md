---
# 1. Add tags
# 2. Add title

# Note: Avoid using 
# i. Special characters (like dashes and speech marks) for note title. 
# ii. Ending in puncutations for  yaml title.  

# Backlinks will populate with waypoint page, to MOC. 

title: "Bash Basic Syntax"
date: 2023-08-19T22:24
enableToc: false
tags:
- bash
- linux
---
### Learning Resources: 
Skimming and pulling creating notes for TILs: 
- [Bash Scripting Tutorial for Beginners (FreeCodeCamp Video)](https://www.youtube.com/watch?v=tK9Oc6AEnR4)
- [Google Style Guide](https://google.github.io/styleguide/shellguide.html)

--- 
### Hello World Scripting
What is the line that all bash scripts need to start with, and why? 
?
A shebang (`#!) declaration is required, so that the system knows what program/shell needs to be used in the running of the script. 
```
#! /bin/bash
```

What permission change is required of bash script files to allow it's functionality? Explain the octal permission system and the common argument for sharing a script. 
?
Bash scripts need to have it's permission set to `executable` for the relevant principal executing. 
A common note, is to use `chmod 755` to only allow others read and execute permissions. 
```
Octal base permissions:

0 = None  
1 = Execute  
2 = Write  
4 = Read

The rest are simply combinations of the base octals:

3 is 1 + 2       // Execute and Write  
5 is 1 + 4       // Execute and Read  
6 is 2 + 4       // Write and Read  
7 is 1 + 2 + 4   // Execute, Write, Readtip: if the number is odd, it includes Execute
```

### Variables and Conditional Arguments

What syntax is used to receive user input to a variable? 
?
`read`
e.g
```
echo First name?
read FIRST_NAME

echo Last name?
read LAST_NAME

echo Hello $FIRST_NAME $LAST_NAME
```

What are positional arguments and what is the `0`-th position reserved for?
?
- Refers to the arguments provided to shell, by commands. 
- The `0`-th argument is reserved for the shell.

What is the syntax to make use of positional arguments?
?
`echo $1 $2` etc.
```sh
#! /bin/bash

echo Hello $1 $2
```

### Output Redirection
How do you redirect script output? 
?
Redirects are done using "`>`".

What is the difference between CTRL + d and CTRL + c in interacting with terminal?
?
- CTRL + c  is an **interrupt**. 
- CTRL + d is a **End of File signal**, often this will log user out of terminal. 

What syntax allows appending text to an existing file, instead of overwriting it?
?
```
cat B.txt >> A+B.txt
```

### Input Redirection

What is a `heredocs`, what is it commonly used with and Why? 
?
- `Heredocs` are multi-line command blocks. 
- Commonly used with `cat`. 
- This is as it allows for the printing of manipulated output/text to screen or to file by redirect. 

What is syntax for use of `Heredocs`?
?
- `Heredocs` use  (`<<`) syntax with a `DELIMITER`.
- This has the effect of **redirecting input from a "file"** that users write into terminal, separated by lines and defined by the delimiters
- Example: 
- Here, we are passing two lines of text containing an [environment variable](https://linuxize.com/post/how-to-set-and-list-environment-variables-in-linux/) and a command to `cat` using a here document.
```bash
# The script will process everything between the delimiters (in this case EOF), as input to the command. 
cat << EOF
The current working directory is: $PWD
You are logged in as: $(whoami)
EOF
```
```output
The current working directory is: /home/linuxize
You are logged in as: linuxize
```
- or through use with "`sort`":
```bash
tommy@tommy-ubuntu-pc:~/Desktop$ sort -d << EOF
> C
> B
> A
> EOF
# output: 
A
B
C
```

What does `<<<` syntax denote?
?
- These are  `herestrings`, similar to heredocs but instead placing the input to be redirected on the same line as the command. 
- `Herestrings` need to be within double-quotes:
```
wc -w <<< "Hello there wordcount!" 
```
```output
# output: 
3
```

What are the different syntax methods to provide input to a command? 
? 
- Redirect `<`
- Heredocs `<<`
- Herestrings `<<<`

### Comments
What is the syntax for comments in bash? 
?
```
# Comments can be like this

: ' 
or even
like
this
for blocks of text
'

```

### Piping
What is piping? What is it's syntax? 
?
Piping is the practice of feeding the output of one command, into another. 
```
ls -l /bin/bin | grep bash
```
This will only show ls results will hence only show results that contain the string "bash". 
### Test Operators
What syntax refers to the exit code of the last command executed? How would you print this to terminal? 
?
- Syntax to refer to last command's exit code / return value is  `$?`
- We can print this to terminal with `echo $?`

What is syntax to incorporate test/evaluation operators to a command? 
?
- We can use square brackets e.g `[ hello = hello]`. 
	- This would evaluate to the successful exit code `0`. 

### Conditionals and Test Expressions (if/elif/else)
How would you syntactically write an `if` comparison statement for a bash script, referencing the first provided argument to the command? 
? 
Example: 
```sh 
#!/bin/bash

if [ ${1,,} = herbert ]; then 
	echo "asserted Herbert!"
elif [ ${1,,} = help ]; then
	echo "Enter your username!" 
else
       echo "Don't recognise user!"
fi

# note: the commas simply denote to lowercase the variable through variable expansion. 

# the following showss
```

What is the equivalent to `len(x)` in bash?
?
- `${#x}`

How do you close `if` statements in bash? 
?
`fi`. 

What is the syntax for **case statements**, noting start, end and new statement syntax. 
?
```sh
#!/bin/bash

case ${1,,} in
	herbert | administrator)
		echo "Hello, you're the boss here!"
		;;
	help)
		echo "Just enter your username!"
		;;
	*)
		echo "Hello there. You're not the boss of me. Enter a valid username!"
esac
```

### Arrays
How do you declare arrays in bash? 
?
` MY_FIRST_ARRAY=("Apple" "Orange" "Banana")`

How would you index into the first item in a bash array? How would you print the WHOLE array? 
?
- Specific index:
	`echo {MY_FIRST_ARRAY}[0]`
- Entire array: 
	`echo {MY_FIRST_ARRAY}[@]`

How do you add items to arrays in bash? What happens when you
?
- You place new values into unused indexes. 

How do you remove items from arrays in bash?
?
You use the `unset` command. 
```bash

unset fruits[2]  # Deletes the element at index 2 (orange)
```

Does bash support slicing?
?
Yes - for example, you can get a range of elements using `${array[start_index:end_index]}`: 
```bash
some_fruits=("${fruits[@]:1:3}")  # Copies elements from index 1 to 3
```

### Bash Functions

What is bash syntax for defining and calling a function?
?
**Definition:**
```bash
# Define a function named "greet"
greet() {
    echo "Hello, welcome to Bash functions!"
}

```
**Example script calling function:**
```bash
#!/bin/bash

hello_world() {
   echo 'hello, world'
}

hello_world
```

How can you pass arguments within script and from terminal, to functions?
? 
- Arguments can only be received from the terminal (through `$1` etc.)
	- Bash does not support **function arguments**, like other languages. 
Example:
```bash 
#!/bin/bash

# Define a function that uses $1 (local argument)
local_function() {
    local local_arg="$1"
    echo "Local argument: $local_arg"
}

# Call the local_function
local_function "LocalArgValue"

# Use $1 (script argument)
echo "Argument from terminal: $1"

---
input:
./example.sh TerminalArgValue

output: 
Local argument: LocalArgValue
Argument from terminal: TerminalArgValue
```
