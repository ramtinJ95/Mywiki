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


### Example
In practice this means that if we want to represent -5 we take 16 - 5 = 11, 11
in binary is 1011 which is the 2's complement representation of -5. 

One shortcut to converting numbers to their negative alternative, i.e x to -x is
to flip all the bits of x and add 1.

Say we have the number 7 in binary that is 0111 so we flip all the bits, i.e
1000 and then we add 1 -> 1001, this is the representation of -7 in 2s
complement. Which we can also see is correct when we take 16 - 7 = 9 and 1001 is
the same as 9. So we can be sure that this shortcut so to say works. 


This shortcut way of converting number to their negative version is what I will
implement in the hardware emulator since its so easy to do. One needs only to
use a not gate and thats it. 
