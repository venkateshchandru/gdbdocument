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
   ```bash
   gdb --tui

2. **View source code:**
   ```bash
   list

3. **View the type of a variable:**
   ```bash
   whatis <variable>

4. **View members of a struct variable:**
   ```bash
   ptype <variable>

5. **Dereference a pointer:**
   ```bash
   * <pointer_name>

6. **Set a temporary breakpoint:**
   ```bash
   tbreak

7. **List all breakpoints:**
   ```bash
   info breakpoints

8. **Delete a breakpoint:**
   ```bash
   delete <breakpoint_num>

9. **Redirect GDB output:**
   ```bash
   tty <path>

10. **Set a conditional breakpoint:**
    ```bash
    b <file_name>:<line_number> if <condition>

11. **Jump directly to execution:**
    ```bash
    advance <function_name or filename:line_num>

12. **Execute until a specific line:**
    ```bash
    until <function_name or filename:line_num>

13. **Watch a variable for changes:**
    ```bash
    watch <variable_name>

14. **Enable/disable a breakpoint:**
    ```bash
    enable <breakpoint_num>
    disable <breakpoint_num>

15. **Save breakpoints to a file:**
    ```bash
    save breakpoints <file_name.txt>

16. **Load breakpoints from a file:**
    ```bash
    source <file_name.txt>

17. **Display changes in a variable:**
    ```bash
    display <variable_name>

18. **View list of displayed variables:**
    ```bash
    info display

19. **Remove a variable from display list:**
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
