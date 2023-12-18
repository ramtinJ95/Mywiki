## Module 1: Boolean Functions and Gate Logic

Boolean function synthesis is the act of taking a truth table and looking only
at the final output column. In this column we only care about values which are
true, or 1. For each row that has a one, create a boolean expression that is
true for that row. Then do this for all of the rows with a one and finally OR
them all together. The resulting function will be a boolean function that
represents the entire truth table.

### Theorem
Any Boolean function can be represented using an expression containing AND, OR
and NOT operations.

But we can take it further, in fact one only really needs the AND and NOT gates
to represent any Boolean function. Since using De Morgan's laws we can convert
an OR into an AND.

The simplest function that we can use to build everything else from is the NAND
function. Using only NAND any Boolean function can be represented, which is
truly a remarkable fact.
