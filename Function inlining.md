# Function Inlining
Basically this means that the compiler will just take the function body and
insert it wherever it is called. This is ideal for small functions bodies that
does something in a tight loop. For this to be inlined by the compiler the
function should be defined and implemented in the header file. A classic example
is vector type or vector class where we do vector addition etc which are usually
one liners. And in such cases the compiler would have to generate a function
call which means:
    Set up call stack 
    Jump to function
    Do math
    Return result
    Resume execution

With inlining we skip all of this and just do the operation where its called
