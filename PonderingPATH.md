# Pondering PATH

## The PATH variable
It turns out that the answer to "How does the shell find ls?" is fairly simple. There is a special shell variable, called PATH, that stores a bunch of directory paths in which the shell will search for programs corresponding to commands. If you blank out the variable, things go badly:
```
hacker@dojo:~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:~$ PATH=""
hacker@dojo:~$ ls
bash: ls: No such file or directory
hacker@dojo:~$
```
Without a PATH, bash cannot find the ls command.

In this level, you will disrupt the operation of the /challenge/run program. This program will DELETE the flag file using the rm command. However, if it can't find the rm command, the flag will not be deleted, and the challenge will give it to you! Thus, you must make it so that /challenge/run also can't find the rm command!

Keep in mind: /challenge/run will be a child process of your shell, so you must apply the concepts you learned in Shell Variables to mess with its PATH variable! If you don't succeed, and the flag gets deleted, you will need to restart the challenge to try again!

### Solve
**Flag:** `pwn.college{IHAW73g7AFJc6pqC9ivFN_t7kSO.QX2cDM1wCN2gjNzEzW}`

I cleared the variable PATH and ran /challenge/run to get the flag.
```
hacker@path~the-path-variable:~$ PATH=""
hacker@path~the-path-variable:~$ /challenge/run
Trying to remove /flag...
/challenge/run: line 4: rm: No such file or directory
The flag is still there! I might as well give it to you!
pwn.college{IHAW73g7AFJc6pqC9ivFN_t7kSO.QX2cDM1wCN2gjNzEzW}
```

### New Learnings
I learnt about the PATH variable and how it stores the paths for important programs.

### References

## Setting PATH
Okay, so things break when you blank out PATH. But what about doing something useful with PATH?

Let's explore how we would, for example, add a new directory of programs to our command repertoire. Recall that PATH stores a list of directories to find commands in and, for commands in nonstandard places, we must typically execute them via their path:
```
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ goodscript
bash: goodscript: command not found
hacker@dojo:~$ /home/hacker/scripts/goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
If you maintain useful scripts that you want to be able to launch by bare name, this is annoying. However, by adding directories to or replacing directories in this list, you can expose these programs to be launched using their bare name! For example:
```
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
Let's practice. This level's /challenge/run will run the win command via its bare name, but this command exists in the /challenge/more_commands/ directory, which is not initially in the PATH. The win command is the only thing that /challenge/run needs, so you can just overwrite PATH with that one directory. Good luck!

### Solve
**Flag:** `pwn.college{gvYTJII4FBTBJvXyYdbRpXZtRXA.QX1cjM1wCN2gjNzEzW}`

I added the more_commands directory to PATH variable and directly ran /challenge/run.
```
hacker@path~setting-path:~$ PATH=/challenge/more_commands/
hacker@path~setting-path:~$ /challenge/run
Invoking 'win'....
Congratulations! You properly set the flag and 'win' has launched!
pwn.college{gvYTJII4FBTBJvXyYdbRpXZtRXA.QX1cjM1wCN2gjNzEzW}
```

### New Learnings
I learnt how to add directories to PATH variable.

### References

## Finding commands
When you type the name of a command, something inside one of the many directories listed in your $PATH variable is what actually gets executed (of course, unless the command is a builtin!). But which file, precisely? You can find out with the aptly-named which command:
```
hacker@dojo:~$ which cat
/bin/cat
hacker@dojo:~$ /bin/cat /flag
YEAH
hacker@dojo:~$
```
Mirroring what the shell does when searching for commands, which looks at each directory in $PATH in order and prints the first file it finds whose name matches the argument you passed.

In this challenge, we added a win command somewhere in your $PATH, but it won't give you the flag. Instead, it's in the same directory as a flag file that we made readable by you! You must find win (with the which command), and cat the flag out of that directory!

### Solve
**Flag:** `pwn.college{gWD8tUUclQ5qZ3UGns1-2OpQCgo.01NzEzNxwCN2gjNzEzW}`

I searched for the directory win is located in and called the flag using its absolute path.
```
hacker@path~finding-commands:~$ which win
/challenge/paths/27369/win
hacker@path~finding-commands:~$ ls /challenge/paths/27369
flag  win
hacker@path~finding-commands:~$ cat /challenge/paths/27369/flag
pwn.college{gWD8tUUclQ5qZ3UGns1-2OpQCgo.01NzEzNxwCN2gjNzEzW}
```

### New Learnings
I learnt about the which command using which you can search what directories are being referred to by PATH.

### References

## Adding commands
Recall our example from the previous level:
```
hacker@dojo:~$ ls /home/hacker/scripts
goodscript	badscript	okayscript
hacker@dojo:~$ PATH=/home/hacker/scripts
hacker@dojo:~$ goodscript
YEAH! This is the best script!
hacker@dojo:~$
```
What we see here, of course, is the hacker making the shell more useful for themselves by bringing their own commands to the party. Over time, you might amass your own elegant tools. Let's start with win!

Previously, the win command that /challenge/run executed was stored in /challenge/more_commands. This time, win does not exist! Recall the final level of Chaining Commands, and make a shell script called win, add its location to the PATH, and enable /challenge/run to find it!

### Solve
**Flag:** `pwn.college{4rl5MfHFMgO5V3mJrRnKt5rIRWo.QX2cjM1wCN2gjNzEzW}`

I used the read command to cat the flag. I made win executable and pointed the PATH to the home directory to call win.
```
hacker@path~adding-commands:~$ touch win
hacker@path~adding-commands:~$ echo 'read FLAG < /flag' > win
hacker@path~adding-commands:~$ echo 'echo $FLAG' >> win
hacker@path~adding-commands:~$ chmod a+x win
hacker@path~adding-commands:~$ PATH=.
hacker@path~adding-commands:~$ /challenge/run
Invoking 'win'....
pwn.college{4rl5MfHFMgO5V3mJrRnKt5rIRWo.QX2cjM1wCN2gjNzEzW}
```

### New Learnings
I practiced how to add PATHs and create our own commands.

### References

## Hijacking commands
Armed with your knowledge, you can now carry out some shenanigans. This challenge is almost the same as the first challenge in this module. Again, this challenge will delete the flag using the rm command. But unlike before, it will not print anything out for you.

How can you solve this? You know that rm is searched for in the directories listed in the PATH variable. You have experience creating the win command when the previous challenge needed it. What else can you create?

### Solve
**Flag:** `pwn.college{g8VgG34wn7w_c3Kqe5vOfLdJVU3.QX3cjM1wCN2gjNzEzW}`

I changed the rm command to print out the file instead of deleting it.
```
hacker@path~hijacking-commands:~$ which rm
/run/dojo/bin/rm
hacker@path~hijacking-commands:~$ touch rm
hacker@path~hijacking-commands:~$ echo 'read FLAG < /flag' > rm
hacker@path~hijacking-commands:~$ echo 'echo $FLAG' >> rm
hacker@path~hijacking-commands:~$ chmod a+x rm
hacker@path~hijacking-commands:~$ PATH=.
hacker@path~hijacking-commands:~$ /challenge/run
Trying to remove /flag...
pwn.college{g8VgG34wn7w_c3Kqe5vOfLdJVU3.QX3cjM1wCN2gjNzEzW}
```

### New Learnings
I learnt that you can change what certain commands do by redirecting the PATH to a different file with the same name.

### References
