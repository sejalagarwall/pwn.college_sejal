# Comprehending Commands

## Cat: not the pet, but the command!
One of the most critical Linux commands is cat. cat is most often used for reading out files, like so:

hacker@dojo:/~$ cat /challenge/DESCRIPTION.md
One of the most critical Linux commands is `cat`.
`cat` is most often used for reading out files, like so:
cat will concatenate (hence the name) multiple files if provided multiple arguments. For example:

hacker@dojo:\~$ cat myfile
This is my file!
hacker@dojo:\~$ cat yourfile
This is your file!
hacker@dojo:\~$ cat myfile yourfile
This is my file!
This is your file!
hacker@dojo:\~$ cat myfile yourfile myfile
This is my file!
This is your file!
This is my file!
Finally, if you give no arguments at all, cat will read from the terminal input and output it. We'll explore that in later challenges...

In this challenge, I will copy the flag to the flag file in your home directory (where your shell starts). Go read it with cat!

### Solve
**Flag:** `pwn.college{Ya3Ue-nr7etYsUtU8-JeGCdPGGG.QXxcTN0wCN2gjNzEzW}`

I read the file 'flag' using the cat command and got the flag.
```
hacker@commands~cat-not-the-pet-but-the-command:~$ cat flag
pwn.college{Ya3Ue-nr7etYsUtU8-JeGCdPGGG.QXxcTN0wCN2gjNzEzW}
```

### New Learnings
I got a basic understanding of the cat command. It reads the content of the file, concatenates multiple files and can also read input from the terminal if no argument is entered.

### References

## 
