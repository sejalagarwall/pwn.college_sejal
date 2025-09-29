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

