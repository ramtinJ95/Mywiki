* For changing which key maps to esc when esc does not work in a VM:
In normal mode do :inoremap jj <esc>

* Vim built in spelling check usage: z= pops open a suggestions list of
spellings, choose with numbers which one you want. 
- If misspelling the same word
the same way then fix the spelling with z= then do :spellr to fix all the same
spelling mistakes in the current buffer. 
- If you want to add a word that does not exist in the dictionary you can do zg
to add it to list of items that are allowed.
