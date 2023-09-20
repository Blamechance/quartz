---
# 1. Add tags
# 2. Add title

# Note: Avoid using 
# i. Special characters (like dashes and speech marks) for note title. 
# ii. Ending in puncutations for  yaml title.  

# Backlinks will populate with waypoint page, to MOC. 

title: "bash-awk"
date: 2023-08-19T22:23
enableToc: true
tags:
- bash
---


##### Resources: 
- [GeeksforGeeks - `awk`](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/)

---
# Usecase: 
`awk` is a scripting language that allows text manipulation, but also arithmetic and conditional logic. 
It's commonly used to:
- Validate/search through text
- Transforming text input, and thus producing formatted text files. 
- Performing calculations
- Looping through data and applying conditional logic. 

**TL;DR:**
- `awk` runs line by line. Each line will be split into fields, represented by each string (if delimited by space). 
- The delimiter of what represents a "line" or "field" can be changed. 
- `awk` is capable of arithmetic, often by using variable assignment also. 
- `awk` is also capable of `if-else`, `for` and `while` logic. 
# Syntax: 
## Basic syntax:
```sh
awk options 'selection _criteria {action }' input-file > output-file
```

- `selection_criteria` is used to pattern match against fields (strings). 
- The pattern to be matched is denoted by single quotes (`''`). 
- Examples of `{actions}` include: 
	- `print`: print the field. 
	- `printf`: formatted printing similar to python. 
	- `delete`: can be used to delete both fields and lines. 

# Quick Cheatsheet: 
|                       **Description**                                         |                     **Syntax**                                                                           |
| -------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| Replace all occurrences of a pattern with a replacement string | `{print $0 ~ /pattern/ ? replacement : $0}`                                                    |
| Delete all lines that match a pattern                          | `{if ($0 ~ /pattern/) next; print $0}`                                                         |
| Print only the lines that match a pattern                      | `{if ($0 ~ /pattern/) print $0}`                                                               |
| Insert a line before or after the line that matches a pattern  | `{if ($0 ~ /pattern/) {print line; print $0}}` or `{if ($0 ~ /pattern/) print $0; print line}` |
| Append a line to the end of the file                           | `{print line}`                                                                                 |
| Change the delimiter from white space to another character   | `awk -F'new_char_here' '{ command }' file.txt`                                                 |
| To only print the last field per line, use `$NF`           | `awk '{print $NF }' file.txt`                                                                                   |

**Common commands/arguments:**
*Example syntax incorporation:*
```sh
#print the first and last fields
awk '{print $1,$NF}' employee.txt

#print all lines, with line numbers
awk '{print NR,$0}' employee.txt 

#print lines from 3 to 6
awk 'NR==3, NR==6 {print NR,$0}' employee.txt

#count the number of lines in a file
awk 'END { print NR }' test.txt

```


***
# User-defined and  Shell Generated Variables
**`END`**: 
	- `END` is a special block used to specify an action once all records are processed. It's useful when looking to validate an entire file, such as by counting number of lines. 

**Positional variables:** 
	- When Awk processes a line/record, it will split each delimited set of characters (string) into variables. 
	- "`$1`", "`$2`", "`$3`" etc. refer to each field within the record -- it is **NOT** zero-indexed. 
	- "`$0`" refers to the entire input record (or line) in "awk". 

**Variable assignment**:
```sh
# syntax:
variable_name=value

# e.g:
awk '{ name = $1; age = $2; print "Name:", name, "Age:", age }' data.txt

# you can also declare variables with defined values, prior to processing: 
awk -v age=25 '{ print "Age:", age }' data.txt

```

**Common special variables:**
- **NR:** NR command keeps a current count of the number of input records.
- **NF:** NF command keeps a count of the number of fields within the current input record.
- **FS:** FS command contains the field separator character which is used to divide fields on the input line. The default is “white space”, meaning space and tab characters. 
- **RS:** RS command stores the current record separator character. Since, by default, an input line is the input record, the default record separator character is a newline.
- **OFS:** OFS command stores the output field separator, which separates the fields when Awk prints them. The default is a blank space. 
# Deleting with `awk`
`awk` can be used to delete both fields or lines. 

**Deleting per pattern:**
```sh
#The following command will delete all lines that contain the word "foo":
awk '/foo/ delete' input.txt
```

**Deleting per positional variable:**
```sh
#The following deletes the second field from each line, but only after printing it first:
awk '/foo/ {print $2} delete $1' input.txt
```

*Notes:*
- The `delete` action is applied after all other awk actions have been executed.
- It only be used to delete fields or records that have already been created.
- It cannot delete fields or records that are created by other awk actions, such as  `split`.

# Conditional logic: 
**Example if-else logic:**
```sh
awk '{  
if(condition_here)  
{  
print "condition matched!"  
}  
else  
{  
print "condition not matched!"  
}  
   
}' sample_data.txt
```

