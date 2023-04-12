## Bash/Unix commands
If you want to rename all the files in a dir that does not contain any spaces
use this one liner

```bash

ls | xargs -I {} mv {} Unix_{}

```
