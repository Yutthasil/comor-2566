# Compiler

A compiler is a special program that translates a programming language's source code into machine code, bytecode or another programming language. The source code is typically written in a high-level, human-readable language such as Java or C++. A programmer writes the source code in a code editor or an integrated development environment (IDE) that includes an editor, saving the source code to one or more text files. A compiler that supports the source programming language reads the files, analyzes the code, and translates it into a format suitable for the target platform.

The program written in a high-level language is known as a source program, and the program converted into a low-level language is known as an object (or target) program. Without compilation, no program written in a high-level language can be executed. For every programming language, we have a different compiler; however, the basic tasks performed by every compiler are the same. The process of translating the source code into machine code involves several stages, including lexical analysis, syntax analysis, semantic analysis, code generation, and optimization.

## How does a compiler work?
Compilers vary in the methods they use for analyzing and converting source code to output code. Despite their differences, they typically carry out the following steps:

* ***Lexical analysis.*** The compiler splits the source code into lexemes, which are individual code fragments that represent specific patterns in the code. The lexemes are then tokenized in preparation for syntax and semantic analyses.

* ***Syntax analysis.*** The compiler verifies that the code's syntax is correct, based on the rules for the source language. This process is also referred to as parsing. During this step, the compiler typically creates abstract syntax trees that represent the logical structures of specific code elements.

* ***Semantic analysis.*** The compiler verifies the validity of the code's logic. This step goes beyond syntax analysis by validating the code's accuracy. For example, the semantic analysis might check whether variables have been assigned the right types or have been properly declared.

* ***IR code generation.*** After the code passes through all three analysis phases, the compiler generates an intermediate representation (IR) of the source code. The IR code makes it easier to translate the source code into a different format. However, it must accurately represent the source code in every respect, without omitting any functionality.

* ***Optimization.*** The compiler optimizes the IR code in preparation for the final code generation. The type and extent of optimization depends on the compiler. Some compilers let users configure the degree of optimization.

* ***Output code generation.*** The compiler generates the final output code, using the optimized IR code.
- - - -
## Linux Compiler
### GCC

In Linux, the GCC stands for GNU Compiler Collection. It is a compiler system for the various programming languages. It is mainly used to compile the C and C++ programs. It takes the name of the source program as a necessary argument; rest arguments are optional such as debugging, warning, object file, and linking libraries.

GCC is a portable tool, and it can run on many operating systems. Also, it can be ported to Windows by using some tools such as Cygwin, MinGW, and MinGW-W64. As it is a key component of GNU toolchain, it contains the following components for developing applications and operating systems:

### GCC Compiler Process

![gcc_process](https://github.com/KanNattawat/Comor-Project-image/blob/main/Pre-Processor%20(1).png?raw=true)

* ***Pre-Processing*** is the first step of the compiling process. In this process, the header files are searched and copied to the source code file. It removes comments, expands macros, and includes files.

* ***Compilation*** process runs the code into the GCC module. In this step, the preprocessed files are converted into assembly language which is just an intermediate-level human readable language. The main purpose is to communicate with the hardware.

* ***Assembly*** process converts the assembly code into binary, machine language code. In this step, all the machine starts to understand the program’s instructions.

*  ***Linking*** is the last step in the whole compiling step. In this step, all the source codes are merged and even the library functions are considered. There’s also dynamic linking where the codes are not copied but binary file names are put inside the code.
----
### Install GCC Compiler
To install the GCC open the terminal on Linux.
The terminal takes the input from the user in the form of commands and displays the output on the screen. Hence we have to pass some commands to install the GCC.
<br />

1. The very first step is to update the packages. This command is used to download package information from all configured sources and to get the info of the updated versions of the packages.

```
sudo apt-get update
```

<br />
<p align="center">
            <img src="https://github.com/KanNattawat/Comor-Project-image/blob/main/gcc_install1.png?raw=true" />
</p>
<br />
<br />
2. Now we have to install the build-essential packages, which is also known as a meta-package, it contains the GCC compiler all the other essentials used to compile the software written in C and C++ language.
<br />
<br />

```
sudo apt install build-essential
```

<br />
<br />

3. Now press `y` to continue gcc install or press `n` to abort an install.

<p align="center">
            <img src="https://github.com/KanNattawat/Comor-Project-image/blob/main/gcc_install2.png?raw=true" />
</p>
<br />
<br />
4. After the second command it will install GCC on your Linux, to verify it is installed correctly, check the version of the GCC.
<br />
<br />

```
gcc --version
```

<br />
<p align="center">
            <img src="https://github.com/KanNattawat/Comor-Project-image/blob/main/gcc_install3.png?raw=true" />
</p>

Now, we have successfully installed the GCC on Linux.

<br />

----
### GCC Command
* ***gcc:*** This is the command itself.
In Linux, the gcc command is used to compile C and C++ programs. Below is a basic syntax along with some common options:

      gcc [options] [source files] [-o output file]

Here's what each part means:
* `gcc` : This is the command itself.

* `[options]` : These are optional flags that modify the behavior of the compiler. Options are preceded by a hyphen (-). Some common options include
  * `-c` : Compile or assemble the source files, but do not link.
  *  `-o` : Specify the name of the output file.
  *  `-Wall` : Enable all warning messages.
  *  `-g` : Generate debugging information.

* `[source files]` : These are the source files (C or C++ files) that you want to compile.
* `[-o output file]` : This option specifies the name of the output file. If omitted, the default output file is usually a.out.
----
### Example of GCC Compiler

This program is a simple one that prints "Hello, world!" to the screen using the printf() function from the stdio.h library and returns 0 when the program finishes execution with the return 0; statement.

#### C Language

``` c
// This code is on hello.c file.

int main() {
    printf("Hello, world!\n");
    return 0;
}
```

<br />


The result of this compilation is the creation of an executable file named `my_program` from the `hello.c`

```
 gcc hello.c -o my_program
```

<br />

We can then run it using `./my_program` and the expected output on the screen should be `"Hello World"`

```
./my_program
```

<br />

The output of running the compiled program `my_program` would be


<p>
            <img src="https://github.com/KanNattawat/Comor-Project-image/blob/main/c_result.png?raw=true" />
</p>

----

## Interesting matters

### Precautions
* ***Warnings:*** Pay attention to compiler warnings! They often indicate potential bugs or security vulnerabilities. Use options like `-Wall` to enable comprehensive warnings and learn to understand and address them.

* ***Sanitizers:*** Utilize tools like AddressSanitizer (ASan) and UndefinedBehaviorSanitizer (UBSan) to detect memory errors and undefined behavior at compile time. These can help catch subtle bugs before they cause problems in production.

* ***Stay updated:*** Use the latest version of GCC whenever possible. Newer versions often include bug fixes and security patches.

## Bug

* Like any complex software, GCC can have bugs. These can lead to unexpected behavior, compilation errors, or even security vulnerabilities. It's important to report any bugs you encounter to the GCC developers so they can be fixed. <br />
You can find information about known bugs and their status on the GCC bug tracker: [GCC Bugzilla](https://gcc.gnu.org/bugzilla/)
----

# References

https://www.techtarget.com/whatis/definition/compiler

https://www.geeksforgeeks.org/introduction-of-compiler-design/

https://www.javatpoint.com/gcc-linux

https://linuxsimply.com/gcc-linux/

https://gcc.gnu.org/onlinedocs/

https://www.geeksforgeeks.org/how-to-install-gcc-compiler-on-linux/
