# Scripting

Scripting refers to the process of writing scripts, which are sets of instructions or commands that are executed by a computer program or scripting engine. Scripts are typically written in scripting languages, which are high-level programming languages designed for tasks that involve the automation of specific actions or processes.
 > **Scripting** refers to the process of writing scripts, which are sets of instructions or commands that are executed by a computer program or scripting engine. Scripts are typically written in scripting languages, which are high-level programming languages designed for tasks that involve the automation of specific actions or processes.
			 
- Automation : Scripts are commonly used to automate repetitive tasks or processes. For example, a script might be created to automate file backups, data processing, or system maintenance.
- Web Development: In web development, scripting languages like JavaScript are used to create dynamic and interactive elements on websites. These scripts run on the client-side (in the user's browser) and enhance the user experience.
-   System Administration: System administrators use scripts to automate routine tasks such as system backups, log file analysis, and software installations.
-   Game Development: Scripting is frequently employed in game development to control various aspects of the game, including character behavior, game events, and user interactions.
- Data Analysis: Scripts are commonly used in data analysis and scientific computing to process and analyze large datasets efficiently.
- Networking: Scripts can be used for network automation, configuring network devices, monitoring network activity, and other networking tasks.
Scripting languages are often interpreted rather than compiled, meaning that the scripts are executed line by line by an interpreter rather than being translated into machine code beforehand. This provides flexibility and ease of use but can come at the cost of execution speed compared to compiled languages. Examples of scripting languages include Python, Ruby, JavaScript, PowerShell, and Bash. Each scripting language is designed for specific use cases and has its own syntax and features.
 

# **What is a Shell?**

Before jumping into shell scripting, it’s necessary to understand what shell is. A shell is a command language interpreter that executes commands read from the standard input device such as a keyboard or a file to execute programs, create files, etc.

Whenever a user opens up the terminal (a console to a shell), the shell issues a command prompt where you’ll type your input. That input is further executed as you hit the Enter key, displaying the output on the terminal.

You can see below that the kernel communicates between the hardware and software throughout the shell script workflow

## Principle of Scripting

-   Automate Repetitive Tasks:
	Role: Enable the automation of repetitive tasks without the need to repeatedly type commands. This helps save time and reduces errors.
Example: Automating data backups, executing recurring commands, or streamlining routine tasks.

-   System Management:
Role: Facilitate convenient management of Linux systems without directly accessing the Terminal.
Example: User administration, configuring system settings, or installing and updating software.

-   Enhance Efficiency:
Role: Speed up the execution of tasks without waiting for user responses.
Example: Automating processes to complete tasks more quickly and efficiently.

-   Collaborate with Other Programs:
Role: Enable scripts to interact and work in conjunction with other programs on Linux.
Example: Integrating script functionality with existing programs, processing data from other applications, or calling external commands.
Scheduled Tasks with cron job:

## **Shell Scripting**

Usually, shells are interactive, which means they accept commands as input from users and execute them. However, sometimes we want to execute a bunch of commands routinely, so we have to type in all commands each time in the terminal.

As a shell can also take commands as input from file, we can write these commands in a file and can execute them in shell to avoid this repetitive work. These files are called Shell Scripts or Shell Programs. Shell scripts are similar to the batch file in MS-DOS. Each shell script is saved with `.sh` file extension e.g., myscript.sh.

A shell script has syntax just like any other programming language. If you have any prior experience with any programming language like Python, C/C++ etc. It would be very easy to get started with it.

### A shell script comprises the following elements –
-   Shell Keywords – if, else, break etc.
-   Shell commands – cd, ls, echo, pwd, touch etc.
-   Functions
-   Control flow – if..then..else, case and shell loops etc.
### Why do we need shell scripts?
**There are many reasons to write shell scripts:**
-   The command and syntax are exactly the same as those directly entered in the command line, so programmers do not need to switch to entirely different syntax
-   Writing shell scripts are much quicker
-   Quick start
-   Interactive debugging etc.
### Some Advantages of shell scripts
-   The command and syntax are exactly the same as those directly entered in the command line, so programmers do not need to switch to entirely different syntax
-   Writing shell scripts are much quicker
-   Quick start
-   Interactive debugging etc.
### Some Disadvantages of shell scripts
-   Prone to costly errors, a single mistake can change the command which might be harmful.
-   Slow execution speed
-   Design flaws within the language syntax or implementation
-   Not well suited for large and complex task
-   Provide minimal data structure unlike other scripting languages. etc.
Simple demo of shell scripting using Bash Shell
If you work on a terminal, something you traverse deep down in directories. Then for coming few directories up in path we have to execute a command like this as shown below to get to the “python” directory:
**![](https://lh7-us.googleusercontent.com/AeEnH_UZdNXk42X0tqShmVJco1wuwEBGuawiWaFsW_50bskwxkgG9j4g3h2LWjHeb3OlSVGqtox2QS04_P1oYpGBhBte6EN4KtFwOU0t1KBxTy0bmVjP-YP78tXbo0dKhU2rLHw0UZEvEUCZgrzkIeA)**
It is quite frustrating, so why not we can have a utility where we just have to type the name of directory and we can directly jump to that without executing the “cd ../” command again and again. Save the script as “jump.sh”

## USEFUL SHELL SCRIPT TEMPLATE
-   Before learning things systematically, here is a fairly simple script which is very powerful and useful for modifying for many different tasks.  
    ``#!/bin/sh  
    for filename in *.nii.gz ; do  
    fname=`$FSLDIR/bin/remove_ext ${filename}`  
    fslmaths ${fname} -s 2 ${fname}_smooth2  
    mv ${fname}.nii.gz ${fname}_smooth0.nii.gz  
    done``

- **What this does:**
For each image (*.nii.gz) it smooths it to make a new one of the same name but ending in _smooth2 and also renames the unsmoothed image to end with _smooth0
- **How this works:**
- The variable filename is used in a for loop to go through each name matching *.nii.gz
- The variable fname is set to the filename with the ending (e.g. .nii.gz) removed.
  Don't worry about how this works for now - the details will be explained later.
- ${filename} and ${fname} are used to get the values (contents) of the variables
- fslmaths is used to do the smoothing.
- mv is used to do the renaming (notice that .nii.gz is needed here, but not for the fsl tools, as they work with or without the .nii.gz endings).

## SCRIPTING TIPS
> Here are some basic, but useful, tips for writing scripts
- Put in comments (to jog your memory when you write your paper months/years later)
- Put in some echo output commands so that you get some feedback on what your script is doing as it runs
- If your script starts doing something bad (or nothing at all) then use control-C to stop it
- If your script makes new files, changes files or deletes files then start with a version which uses echo in front of the important commands. When you run this version it will just display the commands to the screen so that you can examine them carefully and make sure they are right. Once you are happy with them then remove the echo from in front of these commands and run this version.
- It doesn't hurt to make a backup of key files before running a script, just in case

## Scripting for Windows system administrators
> As a Windows system administrator, you constantly perform many routine
tasks in an effort to manage, maintain, and support your Windows
environment. Occasionally the need will arise to create a script that
[ How to choose the best desktop-as-a-service solution ]
handles a repetitive task in a more efficient way, or gets a piece of information that otherwise would be difficult to find out. It is relatively easy to write scripts with the scripting technologies that Microsoft provides. But if you are like most of us, taking the time to learn all of the facets of a scripting language and the underlying
system requirements is difficult. In this series of articles, I will provide you with a foundation upon which you can successfully develop your scripting skills, and begin writing scripts with a minimal amount of effort and time on your part. Let's start with an overview of the different scripting technologies that Microsoft has provided, and then in the weeks to come, I will touch on each of the technologies in detail, and provide some basic code snippets, along with links to where you can find more detailed information. Microsoft has created four independent, yet highly integrated components that make up a well-rounded set of scripting technologies. These include the Windows Scripting Host (WSH), Visual Basic Scripting Edition (VBScript), Windows Management Interface (WMI), and Active Directory Scripting Interface (ADSI). When combined, these components make up a rich set of tools for developing basic to advanced administrative scripts. Each of these technologies provides you with different tools to develop scripts:
* Windows Scripting Host (WSH) is the scripting engine that creates an environment upon which scripts can execute on a Windows system.
* Visual Basic Scripting Edition (VBScript) is the scripting language, based upon the Visual Basic framework, that actually provides the syntax and program control that you will require within your script (i.e. looping, if-then-else statements, function declarations, variable storage, arrays, etc)
*Windows Management Interface (WMI) provides you with a consistent way to access comprehensive system management information (i.e. hard drive information, file system control, etc.)
* Active Directory Scripting Interface (ADSI) is the technology that allows you to create scripts to administer directories such as Active Directory.
management, but the two most important pieces are VBScript and WSH, because without these two components, you would not be able to take advantage of the features of WMI and ADSI (see Figure 1).


#### **Figure 1**
http://www.itworld.com/image_download/windows_scripting.html

## REFERENCE
[https://www.geeksforgeeks.org/introduction-linux-shell-shell-scripting/] <br>
(https://www.freecodecamp.org/news/shell-scripting-crash-course-how-to-write-bash-scripts-in-linux/)<br>
[https://docs.aic-eec.com/computer-operation-system/zero-to-linux-hero/anatomy-of-linux-system/basic-bash- script)https://www.freecodecamp.org/news/shell-scripting-crash-course-how-to-write-bash-scripts-in-linux/]<br>
[https://docs.aic-eec.com/computer-operation-system/zero-to-linux-hero/anatomy-of-linux-system/basic-bash-script]<br>
[https://www.linuxadictos.com/]<br>
[https://adamtheautomator.com/linux-shell-scripting-tutorial/#What_is_a_Shell]<br>
[https://blog.desdelinux.net/th/bash-%]<br>
