## Bash/Unix commands
If you want to rename all the files in a dir that does not contain any spaces
use this one liner

```bash

ls | xargs -I {} mv {} Unix_{}

```

## Vim motions/commands
- "syy yanks the current line into a register called s that one can paste from by doing "sp, in this way its possible to paste from 1 register and not hav it be overwritten when doing deletes. Note that the lowercase naming of the register, in this case s, can be any letter as long as it does not interfere with the normal vim motions, for example a does not work since it will move you into insert mode. 