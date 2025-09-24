# Pondering Paths

## The Root
Alright, so the filesystem starts at /. Under that, there are a whole mess of other directories, configuration files, programs, and, most importantly, flags. In this level, we've added a program right in /, called pwn, that will give you the flag. All you need to do for this level is to invoke this program!

You can invoke a program by providing its path on the command line. In this case, you'll be giving the exact path, starting from /, so the path would be /pwn. This style of path, one that starts with the root directory, is referred to as an "absolute path".

Start the challenge, launch a terminal, invoke the pwn program using its absolute path, and Capture that Flag! Good luck!

### Solve
**Flag:** `pwn.college{ID-9LZdJ0JUoeJDusrrqjlvKo3Z.QX4cTO0wCN2gjNzEzW}`

I called the program using its absolute path from the root.
```
hacker@paths~the-root:~$ /pwn
BOOM!!!
Here is your flag:
pwn.college{ID-9LZdJ0JUoeJDusrrqjlvKo3Z.QX4cTO0wCN2gjNzEzW}
```

### New Learning
I learnt about Linux using the tree structure to store directories and files. I also got to know more about invoking a program using a path.

### References

## Program and absolute paths
Let's explore a slightly more complicated path! Except for in the previous level, challenges in pwn.college are in the challenge directory and the challenge directory is, in turn, right in the root directory (/). The path to the challenge directory is, thus, /challenge. The name of the challenge program in this level is run, and it lives in the /challenge directory. Thus, the path to the run challenge program is /challenge/run.

This challenge again requires you to execute it by invoking its absolute path. You'll want to execute the run file that is in the challenge directory that is, in turn, in the / directory. If you invoke the challenge correctly, it will give you the flag. Good luck!

### Solve
**Flag:** `pwn.college{0vTo5ONn_FX25lWVLEpzwd9JeFg.QX1QTN0wCN2gjNzEzW}`

I called the program which was located in a different directory using its absolute path.
```
hacker@paths~program-and-absolute-paths:~$ /challenge/run
Correct!!!
/challenge/run is an absolute path! Here is your flag:
pwn.college{0vTo5ONn_FX25lWVLEpzwd9JeFg.QX1QTN0wCN2gjNzEzW}
```

### New Learnings
I learnt about how to invoke a program that is in a directory, which is also in a directory.

### References

## Position thy self
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

hacker@dojo:\~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ~ was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

### Solve
**Flag:** `pwn.college{sZKsStU-MnpWvOlmkr9yfMiwlOL.QX2QTN0wCN2gjNzEzW}`

I entered the path first. It gave me an error and told me the correct directory. Then I changed directories and then executed the same command.
```
hacker@paths~position-thy-self:~$ /challenge/run
Incorrect...
You are not currently in the /var directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-thy-self:~$ cd /var
hacker@paths~position-thy-self:/var$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{sZKsStU-MnpWvOlmkr9yfMiwlOL.QX2QTN0wCN2gjNzEzW}
```

### New Learnings
I learnt that you can change directories and only work in those specific directories.

### References

## Position elsewhere
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

hacker@dojo:\~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ~ was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

### Solve
**Flag:** `pwn.college{4oJfKjbGQM9MvowdqaBCTp6tjIq.QX3QTN0wCN2gjNzEzW}`

I had the same approach as the previous challenge. I had to get the terminal to show me the correct directory and then I had cd to it to get the flag.
```
hacker@paths~position-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /tmp directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-elsewhere:~$ cd /tmp
hacker@paths~position-elsewhere:/tmp$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{4oJfKjbGQM9MvowdqaBCTp6tjIq.QX3QTN0wCN2gjNzEzW}
```

### New Learnings
I learnt that you can change directories and work with different directories using the cd command.

### References

## Position yet elsewhere
The Linux filesystem has tons of directories with tons of files. You can navigate around directories by using the cd (change directory) command and passing a path to it as an argument, as so:

hacker@dojo:\~$ cd /some/new/directory
hacker@dojo:/some/new/directory$
This affects the "current working directory" of your process (in this case, the bash shell). Each process has a directory in which it's currently hanging out. The reasons for this will become clear later in the module.

As an aside, now you can see what the ~ was in the prompt! It shows the current path that your shell is located at.

This challenge will require you to execute the /challenge/run program from a specific path (which it will tell you). You'll need to cd to that directory before rerunning the challenge program. Good luck!

### Solve
**Flag:** `pwn.college{YbmOfz7_QMYVfNLfwpftocY_jt6.QX4QTN0wCN2gjNzEzW}`

I ran the command to get the terminal to show the correct directory to me and then I had to cd to it to execute the command and obtain the flag.
```
hacker@paths~position-yet-elsewhere:~$ /challenge/run
Incorrect...
You are not currently in the /home directory.
Please use the `cd` utility to change directory appropriately.
hacker@paths~position-yet-elsewhere:~$ cd /home
hacker@paths~position-yet-elsewhere:/home$ /challenge/run
Correct!!!
/challenge/run is an absolute path, invoked from the right directory!
Here is your flag:
pwn.college{YbmOfz7_QMYVfNLfwpftocY_jt6.QX4QTN0wCN2gjNzEzW}
```

### New Learnings
I learnt that you can change directories using the cd command.

### References

## Implicit relative paths, from /
Now you're familiar with the concept of referring to absolute paths and changing directories. If you put in absolute paths everywhere, then it really doesn't matter what directory you are in, as you likely found out in the previous three challenges.

However, the current working directory does matter for relative paths.

A relative path is any path that does not start at root (i.e., it does not start with /).
A relative path is interpreted relative to your current working directory (cwd).
Your cwd is the directory that your prompt is currently located at.
This means how you specify a particular file, depends on where the terminal prompt is located.

Imagine we want to access some file located at /tmp/a/b/my_file.

If my cwd is /, then a relative path to the file is tmp/a/b/my_file.
If my cwd is /tmp, then a relative path to the file is a/b/my_file.
If my cwd is /tmp/a/b/c, then a relative path to the file is ../my_file. The .. refers to the parent directory.
Let's try it here! You'll need to run /challenge/run using a relative path while having a current working directory of /. For this level, I'll give you a hint. Your relative path starts with the letter c 😊

### Solve
**Flag:** `pwn.college{MxUb3IndeqjG17c7s6w-SQfpQj8.QX5QTN0wCN2gjNzEzW}`

I switched directories from ~ to /. Then I called the program using a relative path and got the flag.
```
hacker@paths~implicit-relative-paths-from-:~$ cd /
hacker@paths~implicit-relative-paths-from-:/$ challenge/run
Correct!!!
challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{MxUb3IndeqjG17c7s6w-SQfpQj8.QX5QTN0wCN2gjNzEzW}
```

### New Learnings
I learnt about relative paths and how to access files using relative paths. To access files through a relative path, you need to be in the correct directory.

### References

## Explicit relative paths, from /
Previously, your relative path was "naked": it directly specified the directory to descend into from the current directory. In this level, we're going to explore more explicit relative paths.

In most operating systems, including Linux, every directory has two implicit entries that you can reference in paths: . and ... The first, ., refers right to the same directory, so the following absolute paths are all identical to each other:

/challenge
/challenge/.
/challenge/./././././././././
/./././challenge/././
The following relative paths are also all identical to each other:

challenge
./challenge
./././challenge
challenge/.
Of course, if your current working directory is /, the above relative paths are equivalent to the above absolute paths.

This challenge will get you using . in your relative paths. Get ready!

### Solve
**Flag:** `pwn.college{U0kzN0ryfxUeHeQdHbk4pGOP01P.QXwUTN0wCN2gjNzEzW}`

Initially, I tried calling the program using explicit relative paths without switching directories. It gave me an incorrect answer and I tried again after switching directories. The '.' references the current directory and that is why switching was required.
```
hacker@paths~explicit-relative-paths-from-:~$ cd /
hacker@paths~explicit-relative-paths-from-:/$ ./challenge/run
Correct!!!
./challenge/run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{U0kzN0ryfxUeHeQdHbk4pGOP01P.QXwUTN0wCN2gjNzEzW}
```

### New Learnings
I learnt about entries to refer to directories. '.' is used to refer to the current directory.

### References

## Implicit relative path
In this level, we'll practice referring to paths using . a bit more. This challenge will need you to run it from the /challenge directory. Here, things get slightly tricky.

Linux explicitly avoids automatically looking in the current directory when you provide a "naked" path. Consider the following:

hacker@dojo:\~$ cd /challenge
hacker@dojo:/challenge$ run
This will not invoke /challenge/run. This is actually a safety measure: if Linux searched the current directory for programs every time you entered a naked path, you could accidentally execute programs in your current directory that happened to have the same names as core system utilities! As a result, the above commands will yield the following error:

bash: run: command not found
We'll explore the mechanisms behind this concept later, but in this challenge, we'll learn how to explicitly use relative paths to launch run in this scenario. The way to do this is to tell Linux that you explicitly want to execute a program in the current directory, using . like in the previous levels. Give it a try now!

### Solve
**Flag:** `pwn.college{QBI5dKDj8s737BDAnuUougfSLV4.QXxUTN0wCN2gjNzEzW}`

I changed directories to challenge and then used '.' to reference challenge and tell Linux I am calling a program 'run' from that directory.
```
hacker@paths~implicit-relative-path:/$ cd /challenge
hacker@paths~implicit-relative-path:/challenge$ ./run
Correct!!!
./run is a relative path, invoked from the right directory!
Here is your flag:
pwn.college{QBI5dKDj8s737BDAnuUougfSLV4.QXxUTN0wCN2gjNzEzW}
```

### New Learnings
I learnt that you need to reference the directory using '.' when calling a file in a directory inside a directory. Linux needs this because of a safety measure.

### References

## Home sweet home
Every user has a home directory, typically under /home in the filesystem. In the dojo, you are the hacker user, and your home directory is /home/hacker. The home directory is typically where users store most of their personal files. As you make your way through pwn.college, this is where you'll store most of your solutions.

Typically, your shell session will start with your home directory as your current working directory. Consider the initial prompt:

hacker@dojo:\~$
The ~ in this prompt is the current working directory, with ~ being shorthand for /home/hacker. Bash provides and uses this shorthand because, again, most of your time will be spent in your home directory. Thus, whenever bash sees \~ provided as the start of an argument in a way consistent with a path, it will expand it to your home directory. Consider:

hacker@dojo:\~$ echo LOOK: \~
LOOK: /home/hacker
hacker@dojo:\~$ cd /
hacker@dojo:/$ cd \~
hacker@dojo:\~$ cd \~/asdf
hacker@dojo:\~/asdf$ cd \~/asdf
hacker@dojo:\~/asdf$ cd \~
hacker@dojo:\~$ cd /home/hacker/asdf
hacker@dojo:\~/asdf$
Note that the expansion of \~ is an absolute path, and only the leading \~ is expanded. This means, for example, that \~/\~ will be expanded to /home/hacker/\~ rather than /home/hacker/home/hacker.

Fun fact: cd will use your home directory as the default destination:

hacker@dojo:\~$ cd /tmp
hacker@dojo:/tmp$ cd
hacker@dojo:~$
Now it's your turn to play! In this challenge, /challenge/run will write a copy of the flag to any file you specify as an argument on the commandline, with these constraints:

Your argument must be an absolute path.
The path must be inside your home directory.
Before expansion, your argument must be three characters or less.
Again, you must specify your path as an argument to /challenge/run as so:

hacker@dojo:~$ /challenge/run YOUR_PATH_HERE

### Solve
**Flag:** `pwn.college{sv-k0mrxb0xYxw99UQJ52Blco86.QXzMDO0wCN2gjNzEzW}`

At first I got stuck at what I was supposed to enter as the argument. After a few errors, I understood that I was supposed to use ~ as a home directory at first and then as a file name.
```
hacker@paths~home-sweet-home:~$ /challenge/run ~/~
Writing the file to /home/hacker/~!
... and reading it back to you:
pwn.college{sv-k0mrxb0xYxw99UQJ52Blco86.QXzMDO0wCN2gjNzEzW}
```

### New Learnings
I learnt about home directories and how they are the default directory we work in. '~' expands to /home/hacker and is a shorthand because the user works in the home directory most of the time. 

### References
