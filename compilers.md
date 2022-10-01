# COMPILERS: Principles, Techniques, and Tools

## Chapter 1 : Introduction 

### 1.1 Language Processors
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

**Interpreter caveat**: Compilers as usually faster than interpreters; however, interpreters give better error diagnostics (goes statement by statement).
