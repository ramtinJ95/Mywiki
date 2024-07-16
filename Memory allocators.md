## Memory allocators
This is a fascinating topic. The idea is that thinking at the level of
individual lifetimes and working with the heap where we are creating a new
pointer or a single object using the new keyword is not good. We dont want to be
thinking at such an low level, instead we want to use arena allocators and other
types of allocators so that we dont have to manage memory so granularly but at
the same time still not need a garbage collector. In this way we get the
benefits of GC langugages but none of the downsides.

Great article explaining the arena allocator approach: https://www.rfleury.com/p/untangling-lifetimes-the-arena-allocator

Great series of artciles explaining memory allocation strategies: https://www.gingerbill.org/series/memory-allocation-strategies/

Great video explaining the reason and evolution of a programmer when it comes to
these ideas: https://www.youtube.com/watch?v=xt1KNDmOYqA

Great talk explaining Arena memory allocators:
https://www.youtube.com/watch?v=nZNd5FjSquk (part 1)
https://www.youtube.com/watch?v=CFzuFNSpycI (part 2)
