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
A string is -> Lexeme or token for Lexical Grammars
Its implemented by the -> Scanner for Lexical grammars

A string is -> Expression for Syntactic Grammars
The alpabet is -> Tokens for Syntactic Grammars
Its implemented by the -> Parser for Syntactic Grammars


### Rules for grammars
Grammars represent an infinite set of valid strings, since we cant write down
such a set we will instead create a finite set of rules. If you start with the
rules and use them to generate the string that are in the grammar then such
strings that are generated are called **derivations** because they are derived
from the rules of the grammar. Rules are called **productions** because they
produce strings in the grammar.

Each production i a context-free grammar has a head, its name, and a body, which
describes what it generates. We can think of the body as a list of symbols.
These symbols come in two kinds
- A **terminal** is a letter for the grammars alphabet. One can think of it like
  a literal value. In the syntactic grammar we are defining, the terminals are
  individual lexemes - the tokens coming fro the scanner like if or 1234. These
  symbols are called terminal because in a sense they are end points, they don
  lead to any further moves.
- A **nonterminal** is a named reference to another rule in the grammar. It
  means "play that rule and insert whatever it produces here". In this way, the
  grammer composes.

## Dig deeper concepts for self study
- Chomsky hierarchy

