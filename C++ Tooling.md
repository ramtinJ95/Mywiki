## nvim-lsp clang
In order for the lsp to be able to find 3rd party libraries such as SDL etc a
few steps had to be taken.
1) First the tool bear had to be downloaded. What this tool does is that it
   highjacks the preprocessor and inserts the compile_commands.json file that it
   generates so that the clang lsp knows where to look for all the headers that
   one uses in the project
2) In the make file I had to include -I"/usr/local/include" as a flag to the g++
   compiler so that bear can in turn create the compile_commands.json file with
   the correct paths so that the clang-lsp can use that json file. Also note
   that, that file has to be in the root of the project. 
3) Run "make clean" then "bear -- make" and the json file will be generated. But
   note that the "-I" flag in step 2 has to be in the makefile compile command
   before doing step 3.
4) If using CMake there is no need for bear on small hobby projects to get the
   lsp to work. It is simply enough to just pass the
   -DCMAKE_EXPORT_COMPILE_COMMANDS=ON flag when calling cmake. 

---
Status: :🌱:
tags: [[030 Software Development.md]] - [[C++ Notes.md]]
date: Tue 21 Feb 2023 17:20:51 CET
