# Chapter 1 : Introduction 

## 1.1 Language Processors
A compiler is a program that can read a program in one language *source* and translate it to an equivalent program in another language *target*.
Compilers need to be able to report errors in the source program detected during the translation process.

**A compiler**
source program --> Compiler --> target program

If the target program is an executable machine-language program, it can then be called by the user to process inputs and produce outputs.

**Running Target Program**
input --> Target Program --> output

**An Interpreter**
An *interpreter* is another kind of language processor. Instead of producing a target program as a translation, an interpreter appears to directly execute the operations specified in the source program on inputs supplied by the user.

source program + input --> Interpreter --> output

**Interpreter caveat**: Compilers are usually faster than interpreters; however, interpreters give better error diagnostics (goes statement by statement).

### Example 1.1 : Java
Java language processors combine compilation and interpretation. Java source programs may first be compiled into an intermdediate form called *bytecodes*. The bytecodes are then interpreted by a virtual machine. Code can be compiled independently of interpretation in this arrangement.
*Just in time compilers* translate bytecode into ML immediately before they run the intermediate program to process the input.

**Hybrid Compiler Steps**
1. source program --> Translator
2. Translator --> intermediate program + input
3. Intermediate program + input --> Virtual Machine
4. Virtual Machine --> output

1. In addition to a compiler, several other programs may be required to make an executable. Source code might be divided into submodules/files. Collecting source code can be handled by a *preprocessor / preprocessing* step.
2. The modified source is then sent to a compiler. This might produce assembly code as output for debugging.
3. Assembly code is processed by an *assembler* that produces relocatable machine code as output.

Large programs are compiled in pieces, so relocatable machine code may have to be linked together with other relocatable object files and library files into the code that actually runs on the machine.

- *linker* : resolves external memory addresses, where the code in one file may referto  a location in another file.
- *loader* : puts all of the executable object files into memory for execution.
