# Digesting Documentation

## Learning from documentation
The typical need you'll have for documentation is just to figure out how to use all these dang programs, and a specific case of that is figuring out what arguments to specify on the command line. This module will mostly dig into that concept, as a proxy for figuring out how to use the programs in general. Through the rest of the module, you'll go through various ways of asking the environment for help for the programs, but first, we'll dig into the concept of reading documentation.

The correct usage of programs depends, in a large part, on the proper specification of arguments to them. Recall the -a of ls -a in the hidden files challenge of the Basic Commands module: that -a was an argument that told ls to list out hidden files as well as non-hidden files. Because we wanted to list out hidden files, invoking ls with the -a argument was the correct way to use it in our scenario.

The program for this challenge is /challenge/challenge, and you'll need to invoke it properly in order for it to give you the flag. Let's pretend that this is its documentation:

Welcome to the documentation for /challenge/challenge! To properly run this program, you will need to pass it the argument of --giveflag. Good luck!

Given that knowledge, go get the flag!

### Solve
**Flag:** `pwn.college{UiDKGgbyZNo70AQNNMjJzffUHFd.QX0ITO0wCN2gjNzEzW}`

I followed the given directions and properly used arguments to obtain the flag.
```
hacker@man~learning-from-documentation:~$ /challenge/challenge --giveflag
Correct argument! Here is your flag:
pwn.college{UiDKGgbyZNo70AQNNMjJzffUHFd.QX0ITO0wCN2gjNzEzW}
```

### New Learnings
I learnt that we can use the environment to help us use programs. An arguement is one example that needs documentation.

### References

## Learning complex usage
While using most commands is straightforward, the usage of some commands can get quite complex. For example, the arguments to commands like sed and awk, which we're definitely not getting into right now, are entire programs in an esoteric programming language! Somewhere on the spectrum between cd and awk are commands that take arguments to their arguments...

This sounds crazy, but you've already encountered this with the find level in Basic Commands. find has a -name argument, and the -name argument itself takes an argument specifying the name to search for. Many other commands are analogous.

Here is this level's documentation for /challenge/challenge:

Welcome to the documentation for /challenge/challenge! This program allows you to print arbitrary files to the terminal, when given the --printfile argument. The argument to the --printfile argument is the path of the flag to read. For example, /challenge/challenge --printfile /challenge/DESCRIPTION.md will print out the description of the level!

Given that documentation, go get the flag!

### Solve
**Flag:** `pwn.college{A2H3gx-3AO-jM6iFQv283qVMD7H.QX1ITO0wCN2gjNzEzW}`

I got stuck at the file name where the flag is stored. After a few tries I got that it is stored in /flag like it always is. I obtained the flag using proper arguments with the /challenge/challenge program.
```
hacker@man~learning-complex-usage:~$ /challenge/challenge --printfile /flag
Correct argument! Here is the /flag file:
pwn.college{A2H3gx-3AO-jM6iFQv283qVMD7H.QX1ITO0wCN2gjNzEzW}
```

### New Learnings
I learnt about arguments inside arguments and how they are used. One example was the find command I previously learnt.

### References

