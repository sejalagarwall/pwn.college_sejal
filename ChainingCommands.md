# Chaining Commands

## Chaining with semicolons
The easiest way to chain commands is ;. In most contexts, ; separates commands in a similar way to how Enter separates lines. So, this:
```
hacker@dojo:~$ echo COLLEGE > pwn
hacker@dojo:~$ cat pwn
COLLEGE
hacker@dojo:~$
```
Is roughly the same as this:
```
hacker@dojo:~$ echo COLLEGE > pwn; cat pwn
COLLEGE
hacker@dojo:~$
```
Basically, when you hit Enter, your shell executes your typed command and, after that command terminates, gives you the prompt to input another command. The semicolon is analogous, just without the prompt and with you entering both commands before anything is executed.

Give it a try now! In this level, you must run /challenge/pwn and then /challenge/college, chaining them with a semicolon.

### Solve
**Flag:** `pwn.college{gpX6rTIM-WGV9mqMBlWMyPL-ewf.QX1UDO0wCN2gjNzEzW}`

I chained two commands and got the flag.
```
hacker@chaining~chaining-with-semicolons:~$ /challenge/pwn; /challenge/college
Yes! You chained /challenge/pwn and /challenge/college! Here is your flag:
pwn.college{gpX6rTIM-WGV9mqMBlWMyPL-ewf.QX1UDO0wCN2gjNzEzW}
```

### New Learnings
I learnt how to chain commands using a semi-colon.

### References

## Building on success
You learned about exit codes in the Processes module. Now let's use them to chain commands together!

The && operator allows you to run a second command only if the first command succeeds (in Linux convention, this means it exited with code 0). This is called the "AND" operator because both conditions must be true: the first command must succeed AND then the second command will run. That's super useful for complex commandline workflows where certain actions depend on the success of other actions.

Here's the syntax:
```
hacker@dojo:~$ command1 && command2
```
This means: "Run command1, and IF it succeeds, then run command2."

Some examples:
```
hacker@dojo:~$ touch /home/hacker/file && echo "this will run"
success
this will run
hacker@dojo:~$ touch /file && echo "this will NOT run"
touch: cannot touch '/file': Permission denied
hacker@dojo:~$
```
That second invocation of touch failed because the hacker user does not have write access to /file, so the echo did not run.

In this challenge, you need to chain the programs /challenge/first-success and /challenge/second using the && operator. Try running each command separately first to see what happens (which is that you will not get the flag). But if you chain them with &&, the flag will appear!

### Solve
**Flag:** `pwn.college{U5EJEbOCER2loPFbuGpW0Yii73o.0lM0MDOxwCN2gjNzEzW}`

I chained the two commands using the conditional chaining operator &&.
```
hacker@chaining~building-on-success:~$ /challenge/first-success
hacker@chaining~building-on-success:~$ /challenge/second
Error: /challenge/first-success must be successfully chained with 
/challenge/second using &&
hacker@chaining~building-on-success:~$ /challenge/first-success && /challenge/second
Nice chaining! Flag: pwn.college{U5EJEbOCER2loPFbuGpW0Yii73o.0lM0MDOxwCN2gjNzEzW}
```

### New Learnings
I can chain commands with a condition that the first command has to succeed for the second one to run by using &&.

### References

## Handling failure
You just learned about the && operator, which runs the second command only if the first succeeds. Now let's learn about its opposite: the || operator allows you to run a second command only if the first command fails (exits with a non-zero code). This is called the "OR" operator because either the first command succeeds OR the second command will run.

Here's the syntax:
```
hacker@dojo:~$ command1 || command2
```
This means: "Run command1, and IF it fails, then run command2."

Some examples:
```
hacker@dojo:~$ touch /file || echo "touch failed, so this runs"
touch: cannot touch '/file': Permission denied
touch failed, so this runs
hacker@dojo:~$ touch /home/hacker/file || echo "this will NOT run"
hacker@dojo:~$
```
The || operator is super useful for providing fallback commands or error handling!

In this challenge, you need to chain /challenge/first-failure and /challenge/second using the || operator. Go for it!

### Solve
**Flag:** `pwn.college{8-JCMZRf8hHVHDkScju7mYhbRhW.01M0MDOxwCN2gjNzEzW}`

I used || to chain the two commands.
```
hacker@chaining~handling-failure:~$ /challenge/first-failure || /challenge/second
Nice chaining! Flag: pwn.college{8-JCMZRf8hHVHDkScju7mYhbRhW.01M0MDOxwCN2gjNzEzW}
```

### New Learnings
I learnt about chaining using || which allows the second command to run only if the first one fails.

### References

## Your first shell script
As you combine more and more commands to achieve complex effects, the length of the combined prompt quickly gets really annoying to deal with. When this happens, you can put these commands in a file, called a shell script, and run them by executing the file! For example, consider our semicolon technique:
```
hacker@dojo:~$ echo COLLEGE > pwn; cat pwn
COLLEGE
hacker@dojo:~$
```
We can create a shell script called pwn.sh (by convention, shell scripts are frequently named with a sh suffix):
```
echo COLLEGE > pwn
cat pwn
```
And then we can execute by passing it as an argument to a new instance of our shell (bash)! When a shell is invoked like this, rather than taking commands from the user, it reads commands from the file.
```
hacker@dojo:~$ ls
hacker@dojo:~$ bash pwn.sh
COLLEGE
hacker@dojo:~$ ls
pwn
hacker@dojo:~$
```
You can see that the shell script executed both commands, creating and printing the pwn file.

Now, it's your turn! Same as last level, run /challenge/pwn and then /challenge/college, but this time in a shell script called x.sh, then run it with bash!

### Solve
**Flag:** `pwn.college{cZG5TTKL2FbNaXBeZOmeU1Dg0c3.QXxcDO0wCN2gjNzEzW}`

I got stuck at creating the shell script file and tried the nano methods but those didn't work. I tried it with echo and it worked although not with chaining.
```
hacker@chaining~your-first-shell-script:~$ touch x.sh
hacker@chaining~your-first-shell-script:~$ echo /challenge/pwn > x.sh
hacker@chaining~your-first-shell-script:~$ echo /challenge/college >> x.sh
hacker@chaining~your-first-shell-script:~$ bash x.sh
Great job, you've written your first shell script! Here is the flag:
pwn.college{cZG5TTKL2FbNaXBeZOmeU1Dg0c3.QXxcDO0wCN2gjNzEzW}
```

### New Learnings
I learnt about shell scripts and how to run them.

### References
GeeksforGeeks

## Redirecting script output
Let's try something a bit trickier! You've piped output between programs with |, but so far, this has just been between one command's output and a different command's input. But what if you wanted to send the output of several programs to one command? There are a few ways to do this, and we'll explore a simple one here: redirecting output from your script!

As far as the shell is concerned, your script is just another command. That means you can redirect its input and output just like you did for commands in the Piping module! For example, you can write it to a file:
```
hacker@dojo:~$ cat script.sh
echo PWN
echo COLLEGE
hacker@dojo:~$ bash script.sh > output
hacker@dojo:~$ cat output
PWN
COLLEGE
hacker@dojo:~$
```
All of the various redirection methods work: > for stdout, 2> for stderr, < for stdin, >> and 2>> for append-mode redirection, >& for redirecting to other file descriptors, and | for piping to another command.

In this level, we will practice piping (|) from your script to another program. Like before, you need to create a script that calls the /challenge/pwn command followed by the /challenge/college command, and pipe the output of the script into a single invocation of the /challenge/solve command!

### Solve
**Flag:** `pwn.college{4vNLZo96eQN4EcbnxSGHizh4TXw.QX4ETO0wCN2gjNzEzW}`

I created a script and stored the commands in it. I piped the output to another command and got the flag.
```
hacker@chaining~redirecting-script-output:~$ touch script.sh
hacker@chaining~redirecting-script-output:~$ echo /challenge/pwn > script.sh
hacker@chaining~redirecting-script-output:~$ echo /challenge/college >> script.sh
hacker@chaining~redirecting-script-output:~$ bash script.sh | /challenge/solve
Correct! Here is your flag:
pwn.college{4vNLZo96eQN4EcbnxSGHizh4TXw.QX4ETO0wCN2gjNzEzW}
```

### New Learnings
i learnt how to pipe a script of commands to another command.

### References

## Executable shell scripts
You have written your first shell script, but calling it via bash script.sh is a pain. Why do you need that bash?

When you invoke bash script.sh, you are, of course launching the bash command with the script.sh argument. This tells bash to read its commands from script.sh instead of standard input, and thus your shell script is executed.

It turns out that you can avoid the need to manually invoke bash. If your shell script file is executable (recall File Permissions), you can simply invoke it via its relative or absolute path! For example, if you create script.sh in your home directory and make it executable, you can invoke it via /home/hacker/script.sh or ~/script.sh or (if your working directory is /home/hacker) ./script.sh.

Try that here! Make a shellscript that will invoke /challenge/solve, make it executable, and run it without explicitly invoking bash!

### Solve
**Flag:** `pwn.college{UAwhRg67EeB3h7DzbFbm_kcaBZH.QX0cjM1wCN2gjNzEzW}`

I created a script and made it executable using chmod. I ran the script using its absolute path.
```
hacker@chaining~executable-shell-scripts:~$ touch script.sh
hacker@chaining~executable-shell-scripts:~$ echo /challenge/solve > script.sh
hacker@chaining~executable-shell-scripts:~$ chmod a+x script.sh
hacker@chaining~executable-shell-scripts:~$ ./script.sh
Congratulations on your shell script execution! Your flag:
pwn.college{UAwhRg67EeB3h7DzbFbm_kcaBZH.QX0cjM1wCN2gjNzEzW}
```

### New Learnings
I learnt how to execute scripts straight from their absolute paths.

### References

## Understanding shebangs
You're well on your way to your new life as a shell scripter! However, so far, your shellscripts can only be launched from the shell. Things worked great in the previous level (because you were invoking your script from the bash shell), but they won't work if your script was being invoked by, say, a program written in Python (or any other language).

When a program is invoked in Linux, the Linux kernel first inspects the file to determine how it should be run. This does NOT use the extension (which is why you don't have to name your shell scripts with a .sh extension, or your Python scripts with a .py extension, or so on). Rather, Linux looks at the first few bytes of the file for this information.

There are a bunch of different types of programs, but if the program file starts with the characters #! (often termed a "shebang"), Linux treats the file as an interpreted program, and the contents of the rest of the line as the path to the interpreter. It then invokes the interpreter with the path to the program file as its only argument.

Consider this shell script:
```
#!/bin/bash

echo "Hello Hackers!"
```
This can be executed as:
```
hacker@dojo:~$ chmod a+x script.sh
hacker@dojo:~$ ./script.sh
Hello Hackers!
hacker@dojo:~$
```
When ./script.sh was executed, Linux opened the file, read the first line, extracted /bin/bash as the interpreter, and executed /bin/bash ./script.sh to launch the script!

Note, the shebang line must be the VERY FIRST line of the file - no blank lines or spaces before it!

For this challenge, create a script at /home/hacker/solve.sh that has a proper shebang and outputs "hack the planet". Remember to make it executable, then run /challenge/run to verify your script works correctly!

