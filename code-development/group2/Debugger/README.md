## Debugger ##

### What is a debugger? ###
  A debugger is a software tool used by developers to identify and fix issues in computer programs. It provides a controlled environment for monitoring and analyzing program execution, allowing developers to understand the behavior of their code and diagnose problems.
  Debuggers are essential for software development, helping to streamline the debugging process and improve overall code quality.
### What are the Best Linux Debuggers you can Use on Linux? ###
### GNU Debugger (GDB) ###
The GNU Debugger (GDB) is a highly versatile and widely used debugger for Linux. As an open-source tool, GDB provides developers with an extensive range of features and capabilities to effectively analyze and debug their programs.
####  What can GDB do? ####
  - Set breakpoints: Pause program execution at specific points to examine variables and analyze behavior.
  - Step through code: Execute code line-by-line, inspecting changes and identifying issues.
  - Inspect variables: View values of variables at any point, understanding data flow and potential errors.
  - Modify variables: Change variable values during debugging to test outcomes and pinpoint root causes.
  - Print expressions: Calculate values on the fly using expressions, gaining insights into program logic.
  - Examine memory: Analyze memory contents for potential corruption or unexpected values.
#### How to installing the GDB ####
The GDB have 2 way to install
  1. Installing by Command
     
     ```sudo apt update
     sudo apt install gdb

     # Output:
     # 'Reading package lists... Done'
     # 'Building dependency tree'
     # 'Reading state information... Done'
     # 'gdb is already the newest version (8.1-0ubuntu3).'
     # '0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.'
     ```
     
  2. Installind by Sourcee Code
  
     ``` wget http://ftp.gnu.org/gnu/gdb/gdb-10.2.tar.xz
     tar -xvf gdb-10.2.tar.xz
     cd gdb-10.2
     ./configure
     make
     sudo make install

     # Output:
     # 'config.status: creating Makefile'
     # 'config.status: creating config.h'
     # 'config.status: executing depfiles commands'
     # 'config.status: executing libtool commands'
     # 'Making install in .'
     # 'make[1]: Entering directory '/home/user/gdb-10.2'
     # 'make[2]: Entering directory '/home/user/gdb-10.2'
     # 'make[2]: Nothing to be done for 'install-exec-am'.
     # 'make[2]: Nothing to be done for 'install-data-am'.
     # 'make[2]: Leaving directory '/home/user/gdb-10.2'
     # 'make[1]: Leaving directory '/home/user/gdb-10.2'
     ```
     
#### Useful GDB commands: ####

Start GDB - Go to your Linux command prompt and type “gdb”.

` gdb `

![304](https://github.com/Chinjuku/Code-Development-1/assets/109953279/e97527d7-32b1-4aaa-aa3d-edff8589ac2c)

command | Description 
--------| -----------
run or r|Executes the program from start to end.
break or b | Sets a breakpoint on a particular line.
disable | Disables a breakpoint
enable | Enables a disabled breakpoint
next or n | Executes the next line of code without diving into functions.
step | Goes to the next instruction, diving into the fuction.
list or l | Display the code.
print or p | Displays the value of a variable.
quit or q | Exits out of GDB.
clear | Clars all breakpoints.
continue | Continues normal execution

example:
set a breakpoint : let's introduce a break point, say line 5.


```
(gdb) b 5
Breakpoint 1 at 0x5555555546a8: file test.c, line 5.
(gdb) |
```

if you want to put breakpoint at different lines, you can type "b line_number".

By default "list or l" display only first 10 lines.

#### How to run program with GDB ####
Step 1: Compile and Build program with debugging symbols $ gcc -g main.cYou can see -g flag is provided to compile program. This will generate debug symbols of program.

Step 2: Run program with GDB$ gdb ./test

![307](https://github.com/Chinjuku/Code-Development-1/assets/109953279/bf17e3df-7729-4d39-bd1f-be8fa1c5ee83)

Step 3: Use GDB commands to analyze and debug program.

Step 4: Exit GDB (gdb) quit Type "quit" on GDB prompt to exit GDB.


### The LLDB Debugger ###
LLDB is a next-generation, high-performance debugger. It’s built on top of LLVM/Clang toolchain, and it offers a great debugging experience with extensive language and platform support.

- Maturity: LLDB is still a relatively young debugger compared to GDB, and it may not yet have all the features or stability of GDB.
- Language support: While LLDB supports many languages, its primary focus is on C, C++, Objective-C, and Swift. Support for other languages may be more limited.
- Community: The LLDB community is growing, but it is not yet as large as the GDB community. This may mean that finding help and resources can be more challenging.

#### How to installing the LLDB ####
1. Ubuntu 16.04 
Add the additional package sources:
```sudo apt-get update
  sudo apt-get install wget
  echo "deb http://llvm.org/apt/xenial/ llvm-toolchain-xenial main" | sudo tee /etc/apt/sources.list.d/llvm.list
  echo "deb http://llvm.org/apt/xenial/ llvm-toolchain-xenial-3.9 main" | sudo tee -a /etc/apt/sources.list.d/llvm.list
  wget -O - http://llvm.org/apt/llvm-snapshot.gpg.key | sudo apt-key add -
  sudo apt-get update
```
Install the lldb packages:
```
sudo apt-get install lldb-3.9 python-lldb-3.9
```
To launch lldb:
`lldb-3.9`

2. Ubuntu 18.04 
To install the lldb packages:
```
sudo apt-get update
sudo apt-get install lldb-3.9 llvm-3.9 python-lldb-3.9
```
To launch lldb:
`lldb-3.9`

#### Debugger commands ####
 - **_apropos:_** -- List debugger commands related to a word or subject.
 - **_breakpoint:_** -- Commands for operating on breakpoints (see 'help b' for shorthand.)
 - **_bugreport:_** -- Commands for creating domain-specific bug reports.
 - **_command_** -- Command for managing custom LLDB commands.
 - **_disassemble_** -- Disassemble specified instructions in the current target.  Defaults to the current function for the current thread and stack frame.
 - **_expression_** -- Evaluate an expression on the current thread.  Displays any returned value with LLDB's default formatting.
 - **_frame_** -- Commands for selecting and examing the current thread's stack frames.
 - **_gdb-remote_** -- Connect to a process via remote GDB server.  If no host is specifed, localhost is assumed.
 - **_gui_** -- Switch into the curses based GUI mode.
 - **_help_** -- Show a list of all debugger commands, or give details about a specific command.
 - **_kdp-remote_** -- Connect to a process via remote KDP server.  If no UDP port is specified, port 41139 is assumed.
 - **_language_** -- Commands specific to a source language.
 - **_log_** -- Commands controlling LLDB internal logging.
 - **_memory_** -- Commands for operating on memory in the current target process.
 - **_platform_** -- Commands to manage and create platforms.
 - **_plugin_** -- Commands for managing LLDB plugins.
 - **_process_** -- Commands for interacting with processes on the current platform.
 - **_quit_** -- Quit the LLDB debugger.
 - **_register_** -- Commands to access registers for the current thread and stack frame.
 - **_script_** -- Invoke the script interpreter with provided code and display any results.  Start the interactive interpreter if no code is supplied.
 - **_settings_** -- Commands for managing LLDB settings.
 - **_source_** -- Commands for examining source code described by debug information for the current target process.
 - **_target_** -- Commands for operating on debugger targets.
 - **_thread_** -- Commands for operating on one or more threads in the current process.
 - **_type_** -- Commands for operating on the type system.
 - **_watchpoint_** -- Commands for operating on watchpoints.
 - **_version_** -- Show the LLDB debugger version.

### reference
<details>
<summary>GDB :</summary>
  <p>https://www.geeksforgeeks.org/gdb-step-by-step-introduction/</p>
  <p>https://ioflood.com/blog/install-gdb-command-linux/#:~:text=In%20most%20Linux%20distributions%2C%20the,command%20sudo%20yum%20install%20gdb%20.</p>
  <p>https://www.sourceware.org/gdb/</p>
  <p>https://www.scaler.com/topics/linux-debugger/</p>
</details>

<details>
<summary>LLDB :</summary>
  <p>https://installati.one/install-lldb-ubuntu-20-04/</p>
  <p>https://lldb.llvm.org</p>
  <p>https://gist.github.com/wanyakun/314690093ea195d749fca6869ebf200e</p>
</details>
 
     
