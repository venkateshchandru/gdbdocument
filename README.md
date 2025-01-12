# GCC and GDB Command Reference

This repository provides a comprehensive reference for using GCC (GNU Compiler Collection) and GDB (GNU Debugger) for compiling and debugging C programs.

---

## Table of Contents

- [GCC Commands](#gcc-gnu-compiler-collection)
- [GDB Commands](#gdb-gnu-debugger)
  - [Basic Commands](#basic-commands)
  - [Program Stack Commands](#program-stack-commands)
  - [Debugging Issues](#debugging-issues)
  - [GDB Help](#gdb-help)
  - [Debugging Techniques](#debugging-techniques)
  - [Breakpoints and Commands](#breakpoints-and-commands)
  - [GDB Scripts](#gdb-scripts)
  - [Advanced Commands](#advanced-commands)
  - [GDB UPDATED COMMANDS] (#GDB-UPDATED-COMMANDS)

---

## GCC (GNU Compiler Collection)

### Basic Commands

1. **Compile a C program:**
   ```bash
   gcc main.c -o program

2. **Enable debugging information:**
   ```bash
   gcc -g main.c -o program
   
3. **Enable warnings during compilation:**
   ```bash
   gcc -Wall main.c -o program
   
4. **Treat warnings as errors:**
   ```bash
   gcc -Werror main.c -o program

## GDB (GNU Debugger)

### Basic Commands

1. **Start GDB with a Text User Interface (TUI):**

   shortcut in GDB terminal: ctrl+x+a

   ```bash
   gdb --tui

3. **View source code:**
   ```bash
   list

4. **View the type of a variable:**
   ```bash
   whatis <variable>

5. **View members of a struct variable:**
   ```bash
   ptype <variable>

6. **Dereference a pointer:**
   ```bash
   * <pointer_name>

7. **Set a temporary breakpoint:**
   ```bash
   tbreak

8. **List all breakpoints:**
   ```bash
   info breakpoints

9. **Delete a breakpoint:**
   ```bash
   delete <breakpoint_num>

10. **Redirect GDB output:**
    ```bash
    tty <path>

11. **Set a conditional breakpoint:**
    ```bash
    b <file_name>:<line_number> if <condition>

12. **Jump directly to execution:**
    ```bash
    advance <function_name or filename:line_num>

13. **Execute until a specific line:**
    ```bash
    until <function_name or filename:line_num>

14. **Watch a variable for changes:**
    ```bash
    watch <variable_name>

15. **Enable/disable a breakpoint:**
    ```bash
    enable <breakpoint_num>
    disable <breakpoint_num>

16. **Save breakpoints to a file:**
    ```bash
    save breakpoints <file_name.txt>

17. **Load breakpoints from a file:**
    ```bash
    source <file_name.txt>

18. **Display changes in a variable:**
    ```bash
    display <variable_name>

19. **View list of displayed variables:**
    ```bash
    info display

20. **Remove a variable from display list:**
    ```bash
    undisplay <display_num>

### Program Stack Commands

1. **Backtrace to see the call stack:**
   ```bash
   bt

2. **Finish the current stack frame:**
   ```bash
   finish

3. **Navigate up/down in the call stack:**
   ```bash
   up
   down


### Debugging Issues
1. **Segmentation fault:** Occurs when a program accesses memory it does not own.

2. **Stack overflow:** Happens when there is excessive memory usage in the call stack.

### GDB Help

**Get help for a specific command:**
    ```bash
     help <action>


### Debugging Techniques

1. **Delta debugging:** Use multiple breakpoints to isolate errors.

2. **Calling functions within GDB:**
   ```bash
   call <function_name(arg...)>

3. **Attaching GDB to a running process:**
   ```bash
   #Get process ID:
   ps aux | grep <name>

   #Attach to a process:
   gdb -p <process_id>

   #Detach from a process:
   detach

4. **Handling core dumps:**
   ```bash
   #Set unlimited core dump size:
    sudo ulimit -c unlimited

   #Check core dump size:
    ulimit -c

   #Install necessary packages
    sudo apt install systemd-coredump

   #View core dump files
    coredumpctl dump
    coredumpctl gdb

### Breakpoints and Commands

1. **Set commands to execute automatically at breakpoints:**
   ```bash
   commands <breakpoint_num>
   print <variable>
   bt
   end

### GDB Scripts

1. **Create a script for GDB commands:**
   
   File name: .gdbinit
   Add commands inside the file.

### Advanced Commands

1. **Set a variable value:**
   ```bash
   set var <variable_name> = <value>

2. **Reverse Debugging:**
   ```bash
   target record-full
   reverse-next

3. **Debugging multithreaded programs:**
  
   1. ***View Threads:***
      ```bash
      info threads
   
   2. ***Switch to a specific thread:***
      ```bash
      thread <thread_num>


### GDB UPDATED COMMANDS

1. **Finish executing the current function:**
      ```bash
      finish

2. **Prints the value in hexadecimal:**
      ```bash
       print/x n
      
3. **Directly examing memory: the x command:**
      ```bash
       x &i

4. **Read watchpoint for a variable:**
      ```bash
       rwatch <varaiable>

5. **Read and write watchpoint for a variable:**
      ```bash
       awatch <varaiable>

6. **Set logging into file:**
      ```bash
       set logging on

***Note***
      GDB saves all output from this point in a text file called gdb.txt that resides in the directory in which you are running GDB 

## Core Dump

   A “core dump” is a snapshot of memory at the instant the program crashed, typically saved in a file called “core”.

The core contains the memory contents of the process at the point of the seg-fault including its 
	code segment, 
	data segment, 
	stack segment and 
	heap segment

### 1. Uses of Core Dump Files

-->	Core dumps allow a user to save a crash for later or off-site analysis, or comparison with other crashes.

-->	For embedded computers, it may be impractical to support debugging on the computer itself, so analysis of a dump may take place on a different computer.

### 2. Resource Limits

Every process has various limits associated with it.

      ```bash
       $ man setrlimit

Bash offers a built-in ulimit through which we can edit these.

Core-file max-size (ulimit -c/RLIMIT_CORE) controls the maximum core file size that can be generated when the process snaps.

      ```bash
       $ ulimit -c unlimited

### 3. Where is my core?

The core is dumped in the current working directory of the process.

### 4. What do do with a core file

Core files can be examined with gdb, the GNU debugger.

It can read the crash informations, and display (among other things) the backtrace that leads to the crash.

      ```bash
       $ gdb /path/to/binary /path/to/core/file

After gdb finished to read the input and shows its prompt, execute:
      
      ```bash
       (gdb) backtrace
or 

      ```bash
       (gdb) bt

GDB will then output the backtrace.

### Dumping core from outside the program

One possibility is with gdb, if available. This will let the program running:

      ```bash
       (gdb) attach <pid>
       (gdb) generate-core-file <optional-filename>
       (gdb) detach

Another possibility is to signal the process. This will terminate it, assuming the signal is not caught by a custom signal handler:

      ```bash
       kill -s SIGABRT <pid>

### Dumping core from within the program

      ```bash
       {
       /*
        * Alternative:
        *   char *p = NULL; *p = 0;
        */
         abort();
         }
