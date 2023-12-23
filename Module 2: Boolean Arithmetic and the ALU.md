# Module 2: Boolean Arithmetic and the ALU


## Boolean Arithmetic
Adding boolan numbers is super easy, just start from the right and if add like
normal addition, except if there are 2 ones like:
 0 1
+
 0 1
 
 ----------
 1 0
 
 then the 1 carries over. But if we already had a cary and would get a new carry
 again then we will write down the 1, i.e if there are 3 ones then the result is
 1 like so:
 
  0 1 1
 +
  0 1 1

 ----------
  1 1 0 

## 2's complement
Many different schemes has been developed to deal with how to represent negative
numbers in a computer. But the method/scheme mostly used today is called 2's
complement.

#### Definition of 2's complement
In a binary system with n digit/bits, the 2's complement of the number x is
defined as:

c = 2^n - x if x != 0, otherwise if x is zero the c (2's complement) is also 0.

