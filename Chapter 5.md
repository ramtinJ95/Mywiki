# Crafting interpreters: Chapter 5 Representing Code
In chapter 4 the lexical grammar that we used is called a regular language. That
is fine for a scanner that emits a flat sequence of tokens. But regular
languages are not powerful enough to handle expressions which can nest
aribtrarily deeply.

We need a more powerful tool, that tool is called context-free grammar (CFG). It
is the next heaviest tool in the toolbox of formal grammars. A formal grammar
takes a set of atomic pieces it calls its "alphabet". Then it defines a (usually
infinite) set of "strings" that are "in" the grammar. Each string is a sequence
of "letters" in the alphabet.

The alpabet is -> Characters for Lexical Grammars
The alpabet is -> Tokens for Syntactic Grammars

A string is -> Lexeme or token for Lexical Grammars
A string is -> Expression for Syntactic Grammars

Its implemented by the -> Scanner for Lexical grammars
Its implemented by the -> Parser for Syntactic Grammars

## Dig deeper concepts for self study
- Chomsky hierarchy

