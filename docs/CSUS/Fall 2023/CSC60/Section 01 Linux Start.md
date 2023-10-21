# Shells

A ***shell*** is an interface between you and the kernel of UNIX/Linux.
The ***kernel*** is the center, the core of the OS.

## Get Current Shell
```bash
echo $SHELL
```

## Get Linux Help
```bash
man {command}
```

## Some Linux Commands

### LS:

Purpose: List files in directory.  
Format: ls \[options]\[file-name]
Some Options:  
```bash
-a # List all files, including hidden ones.  
-d # List directory names only, not ordinary files.  
-g # Show group information with listing.  
-l # Show long listing with extended information.  
-r # List in reverse order.  
-s # List in order of increasing size.  
-t # List in order of time, most recent first.  
Examples: ls ls -ra  
ls –l ls -ls
```

### CP

Purpose: Copy a file.  
Format: cp source-file target-file  
```bash
Example: cp my.file file2  
```
Result: There are now two identical files with different names.

### MV

Purpose: Move or rename a file.  
Format: mv source-file target-file  
```bash
Example: mv my.file file2  
```
Result: One file with the target name exists.

### RM
Purpose: Remove a file.  
Format: rm [option] file(s)  
```bash
Option: -i # Ask before deleting. Often the default.  
Example: rm file2, rm –i file2  
```
Result: The file is no longer listed or available.

### Cat 
Purpose: Display or create files.  
Format: cat [source-file] [symbol] [target-file]  
```bash
Examples: 1. cat this.month  
	      2. cat lab2.c  
```
Result: File displayed on the screen, lines echoed on screen