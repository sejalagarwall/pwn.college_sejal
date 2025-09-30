# Practicing Piping

## Redirecting output
First, let's look at redirecting stdout to files. You can accomplish this with the > character, as so:

hacker@dojo:\~$ echo hi > asdf
This will redirect the output of echo hi (which will be hi) to the file asdf. You can then use a program such as cat to output this file:

hacker@dojo:\~$ cat asdf
hi
In this challenge, you must use this output redirection to write the word PWN (all uppercase) to the filename COLLEGE (all uppercase).

### Solve
**Flag:** `pwn.college{0y6YEXBIzom7LHpRSKQ0KYuv3IZ.QX0YTN0wCN2gjNzEzW}`

I redirected the output to file 'COLLEGE' and got the flag.
```
hacker@piping~redirecting-output:~$ echo PWN > COLLEGE
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your 
flag:
pwn.college{0y6YEXBIzom7LHpRSKQ0KYuv3IZ.QX0YTN0wCN2gjNzEzW}
```

### New Learnings
You can redirect outputs and store them in different files.

### References

## Redirecting more output
Aside from redirecting the output of echo, you can, of course, redirect the output of any command. In this level, /challenge/run will once more give you a flag, but only if you redirect its output to the file myflag. Your flag will, of course, end up in the myflag file!

You'll notice that /challenge/run will still happily print to your terminal, despite you redirecting stdout. That's because it communicates its instructions and feedback over standard error, and only prints the flag over standard out!

### Solve
**Flag:** `pwn.college{o-qth6-pfsOkMkzch8a15gHcoeL.QX1YTN0wCN2gjNzEzW}`

I redirected the output of the command to myflag and then read the file out for the flag.
```
hacker@piping~redirecting-more-output:~$ /challenge/run > myflag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{o-qth6-pfsOkMkzch8a15gHcoeL.QX1YTN0wCN2gjNzEzW}
```

### New Learnings
I learnt that you can redirect outputs from commands as well.

### References

## Appending output
A common use-case of output redirection is to save off some command results for later analysis. Often times, you want to do this in aggregate: run a bunch of commands, save their output, and grep through it later. In this case, you might want all that output to keep appending to the same file, but > will create a new output file every time, deleting the old contents.

You can redirect input in append mode using >> instead of >, as so:

hacker@dojo:\~$ echo pwn > outfile
hacker@dojo:\~$ echo college >> outfile
hacker@dojo:\~$ cat outfile
pwn
college
hacker@dojo:$
To practice, run /challenge/run with an append-mode redirect of the output to the file /home/hacker/the-flag. The practice will write the first half of the flag to the file, and the second half to stdout if stdout is redirected to the file. If you properly redirect in append-mode, the second half will be appended to the first, but if you redirect in truncation mode (>), the second half will overwrite the first and you won't get the flag!

Go for it now!

### Solve
**Flag:** `pwn.college{o5kkKljxAOfiCpS_876JquoDlyh.QX3ATO0wCN2gjNzEzW}`

I used >> to append the second half of the flag to the-flag. I read the file using cat command.
```
hacker@piping~appending-output:~$ /challenge/run >> ~/the-flag
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /home/hacker/the-flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] Good luck!

[TEST] You should have redirected my stdout to a file called /home/hacker/the-flag. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
I will write the flag in two parts to the file /home/hacker/the-flag! I'll do 
the first write directly to the file, and the second write, I'll do to stdout 
(if it's pointing at the file). If you redirect the output in append mode, the 
second write will append to (rather than overwrite) the first write, and you'll 
get the whole flag!
hacker@piping~appending-output:~$ cat ~/the-flag
 | 
\|/ This is the first half:
 v 
pwn.college{o5kkKljxAOfiCpS_876JquoDlyh.QX3ATO0wCN2gjNzEzW}
                              ^
     that is the second half /|\
                              |

If you only see the second half above, you redirected in *truncate* mode (>) 
rather than *append* mode (>>), and so the write of the second half to stdout 
overwrote the initial write of the first half directly to the file. Try append 
mode!
```

### New Learnings
You can append outputs to a single file using >>. > clears the previous data and enters the output without appending.

### References

## Redirecting errors
Just like standard output, you can also redirect the error channel of commands. Here, we'll learn about File Descriptor numbers. A File Descriptor (FD) is a number that describes a communication channel in Linux. You've already been using them, even though you didn't realize it. We're already familiar with three:

FD 0: Standard Input
FD 1: Standard Output
FD 2: Standard Error
When you redirect process communication, you do it by FD number, though some FD numbers are implicit. For example, a > without a number implies 1>, which redirects FD 1 (Standard Output). Thus, the following two commands are equivalent:

hacker@dojo:\~$ echo hi > asdf
hacker@dojo:\~$ echo hi 1> asdf
Redirecting errors is pretty easy from this point. If you have a command that might produce data via standard error (such as /challenge/run), you can do:

hacker@dojo:\~$ /challenge/run 2> errors.log
That will redirect standard error (FD 2) to the errors.log file. Furthermore, you can redirect multiple file descriptors at the same time! For example:

hacker@dojo:\~$ some_command > output.log 2> errors.log
That command will redirect output to output.log and errors to errors.log.

Let's put this into practice! In this challenge, you will need to redirect the output of /challenge/run, like before, to myflag, and the "errors" (in our case, the instructions) to instructions. You'll notice that nothing will be printed to the terminal, because you have redirected everything! You can find the instructions/feedback in instructions and the flag in myflag when you successfully pull this off!

### Solve
**Flag:** `pwn.college{YDRAdvJNCtb6jy_a_pLPGrPrgV6.QX3YTN0wCN2gjNzEzW}`

I used > and 2> to redirect output and error messages respectively. Then I read out the myflag file for the flag.
```
hacker@piping~redirecting-errors:~$ /challenge/run > myflag 2> instructions
hacker@piping~redirecting-errors:~$ cat myflag

[FLAG] Here is your flag:
[FLAG] pwn.college{YDRAdvJNCtb6jy_a_pLPGrPrgV6.QX3YTN0wCN2gjNzEzW}
```

### New Learnings
I learnt about File Descriptor numbers and their uses. I also got to know that you can redirect to multiple files at the same time.

### References

## Redirecting input
Just like you can redirect output from programs, you can redirect input to programs! This is done using <, as so:

hacker@dojo:\~$ echo yo > message
hacker@dojo:\~$ cat message
yo
hacker@dojo:\~$ rev < message
oy
You can do interesting things with a lot of different programs using input redirection! In this level, we will practice using /challenge/run, which will require you to redirect the PWN file to it and have the PWN file contain the value COLLEGE! To write that value to the PWN file, recall the prior challenge on output redirection from echo!

### Solve
**Flag:** `pwn.college{wFfE_HfOy6-BA5QfmP8sdGIlozs.QXwcTN0wCN2gjNzEzW}`

I redirected the output from echo to file PWN and then redirected the same file to /challenge/run as input.
```
hacker@piping~redirecting-input:~$ echo COLLEGE > PWN
hacker@piping~redirecting-input:~$ /challenge/run < PWN
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read 
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{wFfE_HfOy6-BA5QfmP8sdGIlozs.QXwcTN0wCN2gjNzEzW}
```

### New Learnings
I learnt that we can redirect input by using <.

### References

## Grepping stored results
You know how to run commands, how to redirect their output (e.g., >), and how to search through the resulting file (e.g., grep). Let's put this together!

In preparation for more complex levels, we want you to:

Redirect the output of /challenge/run to /tmp/data.txt.
This will result in a hundred thousand lines of text, with one of them being the flag, in /tmp/data.txt.
grep that for the flag!

### Solve
**Flag:** `pwn.college{Y5inYqQxwoWpbDOwME9E7YhofAX.QX4EDO0wCN2gjNzEzW}`

I redirected the output to /tmp/data.txt. I assumed the argument format for grep command and searched for "pwn.college" as the flag always contains that keyword.
```
hacker@piping~grepping-stored-results:~$ /challenge/run > /tmp/data.txt
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : /tmp/data.txt
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to a file called /tmp/data.txt. Checking...

[HINT] File descriptors are inherited from the parent, unless the FD_CLOEXEC is set by the parent on the file descriptor.
[HINT] For security reasons, some programs, such as python, do this by default in certain cases. Be careful if you are
[HINT] creating and trying to pass in FDs in python.

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~grepping-stored-results:~$ grep pwn.college /tmp/data.txt
pwn.college{Y5inYqQxwoWpbDOwME9E7YhofAX.QX4EDO0wCN2gjNzEzW}
```

### New Learnings
I learnt about the grep command and how it's useful to search files.

### References

## Grepping live output
It turns out that you can "cut out the middleman" and avoid the need to store results to a file, like you did in the last level. You can do this by using the | (pipe) operator. Standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe. For example:

hacker@dojo:\~$ echo no-no | grep yes
hacker@dojo:\~$ echo yes-yes | grep yes
yes-yes
hacker@dojo:\~$ echo yes-yes | grep no
hacker@dojo:\~$ echo no-no | grep no
no-no
Now try it for yourself! /challenge/run will output a hundred thousand lines of text, including the flag. grep for the flag!

### Solve
**Flag:** `pwn.college{I9i8ZZS7p4kjEIULm0kJwyWwi_O.QX5EDO0wCN2gjNzEzW}`

I used the pipe operator and directly grepped for the flag from the output.
```
hacker@piping~grepping-live-output:~$ /challenge/run | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stdout : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stdout to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stdout!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{I9i8ZZS7p4kjEIULm0kJwyWwi_O.QX5EDO0wCN2gjNzEzW}
```

### New Learnings
I learnt about piping and how it's to skip the storing output step.

### References

## Grepping errors
You know how to redirect errors to a file, and you know how to pipe output to another program, such as grep. But what if you wanted to grep through errors directly?

The > operator redirects a given file descriptor to a file, and you've used 2> to redirect fd 2, which is standard error. The | operator redirects only standard output to another program, and there is no 2| form of the operator! It can only redirect standard output (file descriptor 1).

Luckily, where there's a shell, there's a way!

The shell has a >& operator, which redirects a file descriptor to another file descriptor. This means that we can have a two-step process to grep through errors: first, we redirect standard error to standard output (2>& 1) and then pipe the now-combined stderr and stdout as normal (|)!

Try it now! Like the last level, this level will overwhelm you with output, but this time on standard error. grep through it to find the flag!

### Solve
**Flag:** `pwn.college{IBnPAEkp1oHurN9jL3IKjAOQhUq.QX1ATO0wCN2gjNzEzW}`

I redirected FD2 to FD1 and then grepped through it to search for the flag.
```
hacker@piping~grepping-errors:~$ /challenge/run 2>&1 | grep pwn.college
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge checks for a specific process at the other end of stderr : grep
[INFO] - the challenge will output a reward file if all the tests pass : /challenge/.data.txt

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /challenge/.data.txt file.

[TEST] You should have redirected my stderr to another process. Checking...
[TEST] Performing checks on that process!

[INFO] The process' executable is /nix/store/8b4vn1iyn6kqiisjvlmv67d1c0p3j6wj-gnugrep-3.11/bin/grep.
[INFO] This might be different than expected because of symbolic links (for example, from /usr/bin/python to /usr/bin/python3 to /usr/bin/python3.8).
[INFO] To pass the checks, the executable must be grep.

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{IBnPAEkp1oHurN9jL3IKjAOQhUq.QX1ATO0wCN2gjNzEzW}
```

### New Learnings
I learnt about redirecting of file descriptors to help grep through errors.

### References

## Filtering with grep -v
The grep command has a very useful option: -v (invert match). While normal grep shows lines that MATCH a pattern, grep -v shows lines that do NOT match a pattern:

hacker@dojo:\~$ cat data.txt
hello hackers!
hello world!
hacker@dojo:\~$ cat data.txt | grep -v world
hello hackers!
hacker@dojo:\~$
Sometimes, the only way to filter to just the data you want is to filter out the data you don't want. In this challenge, /challenge/run will output the flag to stdout, but it will also output over 1000 decoy flags (containing the word DECOY somewhere in the flag) mixed in with the real flag. You'll need to filter out the decoys while keeping the real flag!

Use grep -v to filter out all the lines containing "DECOY" and reveal the real flag!

### Solve
**Flag:** `pwn.college{wjcK3KM9W96yiorJbWS_rfyZ2c5.0FOxEzNxwCN2gjNzEzW}`

I filtered the grep command to print only the matches that don't match the given argument (DECOY in this case).
```
hacker@piping~filtering-with-grep-v:~$ /challenge/run | grep -v DECOY
pwn.college{wjcK3KM9W96yiorJbWS_rfyZ2c5.0FOxEzNxwCN2gjNzEzW}
```

### New Learnings
I learnt how to filter out unwanted results from the grep command.

### References

## Duplicating piped data with tee
When you pipe data from one command to another, you of course no longer see it on your screen. This is not always desired: for example, you might want to see the data as it flows through between your commands to debug unintended outcomes (e.g., "why did that second command not work???").

Luckily, there is a solution! The tee command, named after a "T-splitter" from plumbing pipes, duplicates data flowing through your pipes to any number of files provided on the command line. For example:

hacker@dojo:\~$ echo hi | tee pwn college
hi
hacker@dojo:\~$ cat pwn
hi
hacker@dojo:\~$ cat college
hi
hacker@dojo:\~$
As you can see, by providing two files to tee, we ended up with three copies of the piped-in data: one to stdout, one to the pwn file, and one to the college file. You can imagine how you might use this to debug things going haywire:

hacker@dojo:\~$ command_1 | command_2
Command 2 failed!
hacker@dojo:\~$ command_1 | tee cmd1_output | command_2
Command 2 failed!
hacker@dojo:\~$ cat cmd1_output
Command 1 failed: must pass --succeed!
hacker@dojo:\~$ command_1 --succeed | command_2
Commands succeeded!
Now, you try it! This process' /challenge/pwn must be piped into /challenge/college, but you'll need to intercept the data to see what pwn needs from you!

### Solve
**Flag:** `pwn.college{YAQiJOOwB_fpPCXQ-m8kmTRBvLa.QXxITO0wCN2gjNzEzW}`

I duplicated the output in a file called output_1 and then read the file to see the secret argument. I then piped the output and got the flag.
```
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn | tee output_1 | /challenge/college
Processing...
The input to 'college' does not contain the correct secret code! This code 
should be provided by the 'pwn' command. HINT: use 'tee' to intercept the 
output of 'pwn' and figure out what the code needs to be.
hacker@piping~duplicating-piped-data-with-tee:~$ cat output_1
Usage: /challenge/pwn --secret [SECRET_ARG]

SECRET_ARG should be "YAQiJOOw"
hacker@piping~duplicating-piped-data-with-tee:~$ /challenge/pwn --secret YAQiJOOw | /challenge/college
Processing...
Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{YAQiJOOwB_fpPCXQ-m8kmTRBvLa.QXxITO0wCN2gjNzEzW}
```

### New Learnings
I learnt that you can use 'tee' to duplicate outputs.

### References

## Process substitution for input
Sometimes you need to compare the output of two commands rather than two files. You might think to save each output to a file first:

hacker@dojo:\~$ command1 > file1
hacker@dojo:\~$ command2 > file2
hacker@dojo:\~$ diff file1 file2
But there's a more elegant way! Linux follows the philosophy that "everything is a file". That is, the system strives to provide file-like access to most resources, including the input and output of running programs! The shell follows this philosophy, allowing you to, for example, use any utility that takes file arguments on the command line and hook it up to the output of programs, as you learned in the previous few levels.

Interestingly, we can go further, and hook input and output of programs to arguments of commands. This is done using Process Substitution. For reading from a command (input process substitution), use <(command). When you write <(command), bash will run the command and hook up its output to a temporary file that it will create. This isn't a real file, of course, it's what's called a named pipe, in that it has a file name:

hacker@dojo:\~$ echo <(echo hi)
/dev/fd/63
hacker@dojo:\~$
Where did /dev/fd/63 come from? bash replaced <(echo hi) with the path of the named pipe file that's hooked up to the command's output! While the command is running, reading from this file will read data from the standard output of the command. Typically, this is done using commands that take input files as arguments:

hacker@dojo:\~$ cat <(echo hi)
hi
hacker@dojo:\~$
Of course, you can specify this multiple times:

hacker@dojo:\~$ echo <(echo pwn) <(echo college)
/dev/fd/63 /dev/fd/64
hacker@dojo:\~$ cat <(echo pwn) <(echo college)
pwn
college
hacker@dojo:\~$
Now for your challenge! Recall what you learned in the diff challenge from Comprehending Commands. In that challenge, you diffed two files. Now, you'll diff two sets of command outputs: /challenge/print_decoys, which will print a bunch of decoy flags, and /challenge/print_decoys_and_flag which will print those same decoys plus the real flag.

Use process substitution with diff to compare the outputs of these two programs and find your flag!

### Solve
**Flag:** `pwn.college{gOwejwYI-gHFiJs3JBrt20WJjTG.0lNwMDOxwCN2gjNzEzW}`

I used the diff command to print the real flag. I also used <() to directly pipe the output to a temporary file and use it in diff.
```
hacker@piping~process-substitution-for-input:~$ diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)
94a95
> pwn.college{gOwejwYI-gHFiJs3JBrt20WJjTG.0lNwMDOxwCN2gjNzEzW}
```

### New Learnings
I learnt how to store outputs temporarily and use them as arguments in commands.

### References

## Writing to multiple programs
Now you've learned that process substitution can make command output appear as files for reading with <(command). But you can also use process substitution for writing to commands!

You can duplicate data to two files with tee:

hacker@dojo:\~$ echo HACK | tee THE > PLANET
hacker@dojo:\~$ cat THE
HACK
hacker@dojo:\~$ cat PLANET
HACK
hacker@dojo:\~$
And you've used tee to duplicate data to a file and a command:

hacker@dojo:\~$ echo HACK | tee THE | cat
HACK
hacker@dojo:\~$ cat THE
HACK
hacker@dojo:\~$
But what about duplicating to two commands? As tee says in its manpage, it's designed to write to files and to standard output:

TEE(1)                           User Commands                          TEE(1)

NAME
       tee - read from standard input and write to standard output and files
But wait! You just learned that bash can make commands look like files using process substitution! For writing to a command (output process substitution), use >(command). If you write an argument of >(rev), bash will run the rev command (this command reads data from standard input, reverses its order, and writes it to standard output!), but hook up its input to a temporary named pipe file. When commands write to this file, the data goes to the standard input of the command:

hacker@dojo:\~$ echo HACK | rev
KCAH
hacker@dojo:\~$ echo HACK | tee >(rev)
HACK
KCAH
Above, the following sequence of events took place:

bash started up the rev command, hooking a named pipe (presumably /dev/fd/63) to rev's standard input
bash started up the tee command, hooking a pipe to its standard input, and replacing the first argument to tee with /dev/fd/63. tee never even saw the argument >(rev); the shell substituted it before launching tee
bash used the echo builtin to print HACK into tee's standard input
tee read HACK, wrote it to standard output, and then wrote it to /dev/fd/63 (which is connected to rev's stdin)
rev read HACK from its standard input, reversed it, and wrote KCAH to standard output
Now it's your turn! In this challenge, we have /challenge/hack, /challenge/the, and /challenge/planet. Run the /challenge/hack command, and duplicate its output as input to both the /challenge/the and the /challenge/planet commands! Scroll back through the previous challenges "Duplicating piped data with tee" and "Process substitution for input" if you need a refresher on this method.

Trivia!

The observant learner will realize that the following are equivalent:

hacker@dojo:\~$ echo hi | rev
ih
hacker@dojo:\~$ echo hi > >(rev)
ih
hacker@dojo:\~$
More than one way to pipe data! Of course, the second route is way harder to read and also harder to expand. For example:

hacker@dojo:\~$ echo hi | rev | rev
hi
hacker@dojo:\~$ echo hi > >(rev | rev)
hi
hacker@dojo:\~$
That's just silly! The lesson here is that, while Process Substitution is a powerful tool in your toolbox, it's a very specialized tool; don't use it for everything!

### Solve
**Flag:** `pwn.college{4SH5JZuH94Yv0WEVO0fpq7cwyju.QXwgDN1wCN2gjNzEzW}`

At first, I got stuck because I added an extra > which wasn't needed. But after trial and error, I got the right command.
```
hacker@piping~writing-to-multiple-programs:~$ /challenge/hack | tee >(/challenge/the) >(/challenge/planet)
This secret data must directly and simultaneously make it to /challenge/the and 
/challenge/planet. Don't try to copy-paste it; it changes too fast.
1200264333015417023
Congratulations, you have duplicated data into the input of two programs! Here 
is your flag:
pwn.college{4SH5JZuH94Yv0WEVO0fpq7cwyju.QXwgDN1wCN2gjNzEzW}
```

### New Learnings
You can duplicate outputs to multiple commands at the same time with tee and >().

### References

## Split-piping stderr and stdout
Now, let's put your knowledge together. You must master the ultimate piping task: redirect stdout to one program and stderr to another.

The challenge here, of course, is that the | operator links the stdout of the left command with the stdin of the right command. Of course, you've used 2>&1 to redirect stderr into stdout and, thus, pipe stderr over, but this then mixes stderr and stdout. How to keep it unmixed?

You will need to combine your knowledge of >(), 2>, and |. How to do it is a task I'll leave to you.

In this challenge, you have:

/challenge/hack: this produces data on stdout and stderr
/challenge/the: you must redirect hack's stderr to this program
/challenge/planet: you must redirect hack's stdout to this program
Go get the flag!

### Solve
**Flag:** `pwn.college{IfXYuB87cjnu2adJmPTFvL1wty-.QXxQDM2wCN2gjNzEzW}`

I first tried using 2>&1 but that did not work for me. I redirected the error by using >() to make a temporary file. I redirected the output by using |.
```
hacker@piping~split-piping-stderr-and-stdout:~$ /challenge/hack 2> >(/challenge/the) | /challenge/planet
Congratulations, you have learned a redirection technique that even experts 
struggle with! Here is your flag:
pwn.college{IfXYuB87cjnu2adJmPTFvL1wty-.QXxQDM2wCN2gjNzEzW}
```

### New Learnings
I learnt how to redirect error and output at the same time.

### References

## Named pipes
You've learned about pipes using |, and you've seen that process substitution creates temporary named pipes (like /dev/fd/63). You can also create your own persistent named pipes that stick around on the filesystem! These are called FIFOs, which stands for First (byte) In, First (byte) Out.

You create a FIFO using the mkfifo command:

hacker@dojo:\~$ mkfifo my_pipe
hacker@dojo:\~$ ls -l my_pipe
prw-r--r-- 1 hacker hacker 0 Jan 1 12:00 my_pipe
-rw-r--r-- 1 hacker hacker 0 Jan 1 12:00 some_file
hacker@dojo:\~$
Notice the p at the beginning of the permissions - that indicates it's a pipe! That's markedly different than the - that's at the beginning of normal files, such as some_file in the above example.

Unlike the automatic named pipes from process substitution:

You control where FIFOs are created
They persist until you delete them
Any process can write to them by path (e.g., echo hi > my_pipe)
You can see them with ls and examine them like files
One problem with FIFOs is that they'll "block" any operations on them until both the read side of the pipe and the write side of the pipe are ready. For example, consider this:

hacker@dojo:\~$ mkfifo myfifo
hacker@dojo:\~$ echo pwn > myfifo
To service echo pwn > myfifo, bash will open the myfifo file in write mode. However, this operation will hang until something also opens the file in read mode (thus completing the pipe). That can be in a different console:

hacker@dojo:\~$ cat myfifo
pwn
hacker@dojo:\~$
What happened here? When we ran cat myfifo, the pipe had both sides of the connection all set, and unblocked, allowing echo pwn > myfifo to run, which sent pwn into the pipe, where it was read by cat.

Of course, this can somewhat be done by normal files: you've learned how to echo stuff into them and cat them out. Why use a FIFO instead? Here are key differences:

No disk storage: FIFOs pass data directly between processes in memory - nothing is saved to disk
Ephemeral data: Once data is read from a FIFO, it's gone (unlike files where data persists)
Automatic synchronization: Writers block until the readers are ready, and vice-versa. This is actually useful! It provides automatic synchronization. Consider the example above: with a FIFO, it doesn't matter if cat myfifo or echo pwn > myfifo is executed first; each would just wait for the other. With files, you need to make sure to execute the writer before the reader.
Complex data flows: FIFOs are useful for facilitating complex data flows, merging and splitting data in flexible ways, and so on. For example, FIFOs support multiple readers and writers.
This challenge will be a simple introduction to FIFOs. You'll need to create a /tmp/flag_fifo file and redirect the stdout of /challenge/run to it. If you're successful, /challenge/run will write the flag into the FIFO! Go do it!

HINT: The blocking behavior of FIFOs makes it hard to solve this challenge in a single terminal. You may want to use the Desktop or VSCode mode for this challenge so that you can launch two terminals.

### Solve
**Flag:** `pwn.college{8jsDjh3yq3vdqqScQbPJQx9wSuy.01MzMDOxwCN2gjNzEzW}`

I created the fifo and then redirected /challenge/run output to that. I opened a different terminal and then read the fifo to obtain the flag.
```
hacker@piping~named-pipes:~$ mkfifo /tmp/flag_fifo
hacker@piping~named-pipes:~$ /challenge/run > /tmp/flag_fifo
You're successfully redirecting /challenge/run to a FIFO at /tmp/flag_fifo! 
Bash will now try to open the FIFO for writing, to pass it as the stdout of 
/challenge/run. Recall that operations on FIFOs will *block* until both the 
read side and the write side is open, so /challenge/run will not actually be 
launched until you start reading from the FIFO!

hacker@piping~named-pipes:~$ cat /tmp/flag_fifo
You've correctly redirected /challenge/run's stdout to a FIFO at 
/tmp/flag_fifo! Here is your flag:
pwn.college{8jsDjh3yq3vdqqScQbPJQx9wSuy.01MzMDOxwCN2gjNzEzW}
```

### New Learnings
I learnt how to create FIFOs and use them in the terminal.

### References
