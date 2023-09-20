---
# 1. Add tags
# 2. Add title

# Note: Avoid using 
# i. Special characters (like dashes and speech marks) for note title. 
# ii. Ending in puncutations for  yaml title.  

# Backlinks will populate with waypoint page, to MOC. 

title: "bash-find"
date: 2023-08-21T16:58
enableToc: true
tags:
- bash
---

##### Resources: 
- [GeeksforGeeks](https://www.geeksforgeeks.org/find-command-in-linux-with-examples/)

---

# Syntax:

```bash

find [where to start searching from]
 [expression determines what to find] [-options] [what to find]

e.g 
find "$MD_DIRECTORY" -name '*.md' -exec echo "File is: {}" \;
```

- By default, `find` searches recursively to include sub-directories and files too. 
# Cheatsheet: 

| **Description**                                             | **Syntax**                                                       |
| ----------------------------------------------------------- | ---------------------------------------------------------------- |
| Search for all files of a pattern                           | `find ./GFG -name *.txt`                                         |
| Placeholder for "current file path of found object" -> `{}` | `find "$MD_DIRECTORY" -name '*.md' -exec echo "File is: {}" \; ` |
| To run a command after finding a file, use `-exec`          | `find [location] -exec \;`                                       |
| To initiate a loop on a $pattern file, without splitting the lines into fields  |   `while IFS= read -r pattern; do` { code here }                                                             |


- To run defined functions with find -exec, [you need to specify the shell](https://stackoverflow.com/questions/4321456/find-exec-a-shell-function-in-linux) (since only shell can run shell scripts)). 
