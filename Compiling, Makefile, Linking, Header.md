## Header files
The Idea of header files is that they act as the table of contents in a way for
our functions. Header files contain only the proto type of functions and no
implementation. So the header file contains stuff like

  int CountWordsInSentence(const char* sentance);

then we go and include this header in the file that contain the actual
implementation of this function prototype.

#### Important
For every header file it is very important that we add a protection guard
  #ifndef
  #define
  and in the end of the file
  #endif

Reason for this is that in one project it is very likely that we include the
same header files in multiple source files, but we dont want the preprocessor to
append it to multiple files. So with this protection guard pattern we make sure
that the preprocessor only appends each header one time, since it is not
necessary to append it more then once in the entire project. 

## Compiler anatomy
When compiling C and C++ code, the compiling from text file to source code is
not the only thing that happens. There are three major steps:
- Preprocessor: Parses all the code and includes all the content of all the
  includes into the source code. 

- Compiler: Parses the tokens and makes sure syntax is correct and makes sense
  syntactically.
  
- Linker: Here we bundle everything together. Compiler just says that everything
  look ok, but the linker actually goes and fetches all the implementations of
  the functions in the header files. This means that if one has linker errors
  then in the compile command, or in the make file, one has to tell the linker
  which package/implemention to go and link to. For in-depth explanation about
  linkers check out this article series: https://lwn.net/Articles/276782/ its
  supposed to be quite good.


---
Status: :🌳:
[tags](tags): [[C++ Notes.md]]
date: Tue 21 Feb 2023 17:11:55 CET
