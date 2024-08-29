# Crafting interpreters: Chapter 4 notes
Say we have a line like:
var language = "lox";
Lexical analysis is about scanning through a list of characters and grouping
them together into the smalles sequence that still represent something. Each of
these blobs of charcters is called a **Lexeme**. In the example line of lox code
the lexemes are var, language, =, "lox", ;. The lexemes are only the raw
substrings of the soruce code. However in the process of grouping character
sequences into lexemes, we also stumble upon some other useful information. A
lexeme bundled together with that other useful data is a token. 

The parser could categorize tokens from the raw lexeme by comparing the strings, 
but that’s slow and kind of ugly. Instead, at the point that we recognize a lexeme,
we also remember which kind of lexeme it represents. We have a different type for
each keyword, operator, bit of punctuation, and literal type.
