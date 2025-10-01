# Data Manipulation

## Translating characters
One of the purposes of piping data is to modify it. Many Linux commands will help you modify data in really cool ways. One of these is tr, which translates characters it receives over standard input and prints them to standard output.

In its most basic usage, tr translates the character provided in its first argument to the character provided in its second argument:

hacker@dojo:\~$ echo OWN | tr O P
PWN
hacker@dojo:\~$
It can also handle multiple characters, with the characters in different positions of the first argument replaced with associated characters in the second argument.

hacker@dojo:\~$ echo PWM.COLLAGE | tr MA NE
PWN.COLLEGE
hacker@dojo:\~$
Now, you try it! In this level, /challenge/run will print the flag but will swap the casing of all characters (e.g., A will become a and vice-versa). Can you undo it with tr and get the flag?

### Solve
**Flag:** `pwn.college{YaSGxecAoOOvL432STc2ZvJvMpL.01MxEzNxwCN2gjNzEzW}`

I entered all the alphabets twice in different cases so that the case switch happens.
```
hacker@data~translating-characters:~$ /challenge/run | tr AaBbCcDdEeFfGgHhIiJjKkLlM
mNnOoPpQqRrSsTtUuVvWwXxYyZz aAbBcCdDeEfFgGhHiIjJkKlLmMnNoOpPqQrRsStTuUvVwWxXyYzZ
yOUR CASE-SWAPPED FLAG:
pwn.college{YaSGxecAoOOvL432STc2ZvJvMpL.01MxEzNxwCN2gjNzEzW}
```

### New Learnings
I learnt about the tr command and how it's used to replace letters.

### References

## Deleting characters
tr can also translate characters to nothing (i.e., delete them). This is done via a -d flag and an argument of what characters to delete:

hacker@dojo:\~$ echo PAWN | tr -d A
PWN
hacker@dojo:\~$
Pretty simple! Now you give it a try. I'll intersperse some decoy characters (specifically: ^ and %) among the flag characters. Use tr -d to remove them!

