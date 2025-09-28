# File Globbing

## Matching with *
The first glob we'll learn is *. When it encounters a * character in any argument, the shell will treat it as a "wildcard" and try to replace that argument with any files that match the pattern. It's easier to show you than explain:

hacker@dojo:\~$ touch file_a
hacker@dojo:\~$ touch file_b
hacker@dojo:\~$ touch file_c
hacker@dojo:\~$ ls
file_a	file_b	file_c
hacker@dojo:\~$ echo Look: file_*
Look: file_a file_b file_c
Of course, though in this case, the glob resulted in multiple arguments, it can just as simply match only one. For example:

hacker@dojo:\~$ touch file_a
hacker@dojo:\~$ ls
file_a
hacker@dojo:\~$ echo Look: file_*
Look: file_a
When zero files are matched, by default, the shell leaves the glob unchanged:

hacker@dojo:\~$ touch file_a
hacker@dojo:\~$ ls
file_a
hacker@dojo:\~$ echo Look: nope_*
Look: nope_*
The * matches any part of the filename except for / or a leading . character. For example:

hacker@dojo:\~$ echo ONE: /ho*/\*ck\*
ONE: /home/hacker
hacker@dojo:\~$ echo TWO: /\*/hacker
TWO: /home/hacker
hacker@dojo:\~$ echo THREE: ../\*
THREE: ../hacker
Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use globbing to keep the argument you pass to cd to at most four characters! Once you're there, run /challenge/run for the flag!

### Solve
**Flag:** `pwn.college{o5IssQT1ctNHGlVHsQuKGDICB-v.QXxIDO0wCN2gjNzEzW}`

I used * to auto fill /challenge and change directory to it. 
```
hacker@globbing~matching-with-:~$ cd /ch*
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{o5IssQT1ctNHGlVHsQuKGDICB-v.QXxIDO0wCN2gjNzEzW}
hacker@globbing~matching-with-:/challenge$
```

### New Learnings
I learnt how to use * and how it is helpful.

### References

## Matching with ?
Next, let's learn about ?. When it encounters a ? character in any argument, the shell will treat it as a single-character wildcard. This works like *, but only matches one character. For example:

hacker@dojo:\~$ touch file_a
hacker@dojo:\~$ touch file_b
hacker@dojo:\~$ touch file_cc
hacker@dojo:\~$ ls
file_a	file_b	file_cc
hacker@dojo:\~$ echo Look: file_?
Look: file_a file_b
hacker@dojo:\~$ echo Look: file_??
Look: file_cc
Now, practice this yourself! Starting from your home directory, change your directory to /challenge, but use the ? character instead of c and l in the argument to cd! Once you're there, run /challenge/run for the flag!

### Solve
**Flag:** `pwn.college{ssnO-joypKjaySHPZ2hv23tPiY_.QXyIDO0wCN2gjNzEzW}`

I used ? as placeholder for 'c' and 'l' characters to change directories.
```
hacker@globbing~matching-with-:~$ cd /?ha??enge
hacker@globbing~matching-with-:/challenge$ /challenge/run
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{ssnO-joypKjaySHPZ2hv23tPiY_.QXyIDO0wCN2gjNzEzW}
hacker@globbing~matching-with-:/challenge$ 
```

### New Learnings
I learnt about ? and how it is different from *.

### References

## Matching with []
Next, we will cover []. The square brackets are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, or n. For example:

hacker@dojo:\~$ touch file_a
hacker@dojo:\~$ touch file_b
hacker@dojo:\~$ touch file_c
hacker@dojo:\~$ ls
file_a	file_b	file_c
hacker@dojo:\~$ echo Look: file_[ab]
Look: file_a file_b
Try it here! We've placed a bunch of files in /challenge/files. Change your working directory to /challenge/files and run /challenge/run with a single argument that bracket-globs into file_b, file_a, file_s, and file_h!

### Solve
**Flag:** `pwn.college{AGtIW2WcRvd206vRlfCHEqouDG5.QXzIDO0wCN2gjNzEzW}`

I used [] to give the shell limited options to match characters.
```
hacker@globbing~matching-with-:~$ cd /challenge/files
hacker@globbing~matching-with-:/challenge/files$ /challenge/run file_[absh]
You got it! Here is your flag!
pwn.college{AGtIW2WcRvd206vRlfCHEqouDG5.QXzIDO0wCN2gjNzEzW}
```

### New Learnings
I learnt about [] and how it is a limited form of ?.

### References

## Matching paths with []
Globbing happens on a path basis, so you can expand entire paths with your globbed arguments. For example:

hacker@dojo:\~$ touch file_a
hacker@dojo:\~$ touch file_b
hacker@dojo:\~$ touch file_c
hacker@dojo:\~$ ls
file_a	file_b	file_c
hacker@dojo:\~$ echo Look: /home/hacker/file_[ab]
Look: /home/hacker/file_a /home/hacker/file_b
Now it's your turn. Once more, we've placed a bunch of files in /challenge/files. Starting from your home directory, run /challenge/run with a single argument that bracket-globs into the absolute paths to the file_b, file_a, file_s, and file_h files!

### Solve
**Flag:** `pwn.college{A0nPHTYn5TPXGvjVtjBMzWhr19v.QX0IDO0wCN2gjNzEzW}`

I entered the complete file path as an argument to /challenge/run while using [] to limit the files to file_a, file_b, file_s and file_h.
```
hacker@globbing~matching-paths-with-:~$ /challenge/run /challenge/files/file_[absh]
You got it! Here is your flag!
pwn.college{A0nPHTYn5TPXGvjVtjBMzWhr19v.QX0IDO0wCN2gjNzEzW}
```

### New Learnings
I learnt you can use [] in absolute paths as well.

### References

## Multiple globs
So far, you've specified one glob at a time, but you can do more! Bash supports the expansion of multiple globs in a single word. For example:

hacker@dojo:\~$ cat /*fl*
pwn.college{YEAH}
hacker@dojo:\~$
What happens above is that the shell looks for all files in / that start with anything (including nothing), then have an f and an l, and end in anything (including ag, which makes flag).

Now you try it. We put a few happy, but diversely-named files in /challenge/files. Go cd there and run /challenge/run, providing a single argument: a short (3 characters or less) globbed word with two * globs in it that covers every word that contains the letter p.

### Solve
**Flag:** `pwn.college{8mNTU0FnHHpeX49uER0Px23SG7b.0lM3kjNxwCN2gjNzEzW}`

To cover all words with the letter p in it, I used * at the start and end to cover any letters coming before or after p.
```
hacker@globbing~multiple-globs:~$ cd /challenge/files
hacker@globbing~multiple-globs:/challenge/files$ /challenge/run *p*
You got it! Here is your flag!
pwn.college{8mNTU0FnHHpeX49uER0Px23SG7b.0lM3kjNxwCN2gjNzEzW}
```

### New Learnings
I learnt we can use more than one glob in a single sentence and how useful it is in covering different things.

### References

## Mixing globs
Now, let's put the previous levels together! We put a few happy, but diversely-named files in /challenge/files. Go cd there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to /challenge/run) will match the files "challenging", "educational", and "pwning"!

### Solve
**Flag:** `pwn.college{IHX5vE4Ll88Ag60jpuvQmcd8EwI.QX1IDO0wCN2gjNzEzW}`

I tested out a few arguments like \*i\*n\* but that did not work as it did not include []. Then I tried doing [cep]* which worked and I got the flag.
```
hacker@globbing~mixing-globs:~$ cd /challenge/files
hacker@globbing~mixing-globs:/challenge/files$ /challenge/run [cep]*
You got it! Here is your flag!
pwn.college{IHX5vE4Ll88Ag60jpuvQmcd8EwI.QX1IDO0wCN2gjNzEzW}
```

### New Learnings
I revised *, ? and [] placeholders in Linux.

### References

## Exclusionary globbing
Sometimes, you want to filter out files in a glob! Luckily, [] helps you do just this. If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed. For example:

hacker@dojo:\~$ touch file_a
hacker@dojo:\~$ touch file_b
hacker@dojo:\~$ touch file_c
hacker@dojo:\~$ ls
file_a	file_b	file_c
hacker@dojo:\~$ echo Look: file_[!ab]
Look: file_c
hacker@dojo:\~$ echo Look: file_[^ab]
Look: file_c
hacker@dojo:\~$ echo Look: file_[ab]
Look: file_a file_b
Armed with this knowledge, go forth to /challenge/files and run /challenge/run with all files that don't start with p, w, or n!

NOTE: The ! character has a different special meaning in bash when it's not the first character of a [] glob, so keep that in mind if things stop making sense! ^ does not have this problem, but is also not compatible with older shells.

### Solve
**Flag:** `pwn.college{gpQhbWT250cS9WK7JHHo0qj4vEI.QX2IDO0wCN2gjNzEzW}`

I got stuck at what argument to put after /challenge/run. I tried \*[^pwn] but that didn't work because I had to remove the files starting with p, w, and n. I tried [^pwn]\* and that gave me the flag. 
```
hacker@globbing~exclusionary-globbing:~$ cd /challenge/files
hacker@globbing~exclusionary-globbing:/challenge/files$ /challenge/run [^pwn]*
You got it! Here is your flag!
pwn.college{gpQhbWT250cS9WK7JHHo0qj4vEI.QX2IDO0wCN2gjNzEzW}
```

### New Learnings
I learnt how to exclude certain files from the output.

### References

## Tab completion
As tempting as it might be, using * to shorten what must be typed on the commandline can lead to mistakes. Your glob might expand to unintended files, and you might not spot it until the rm command is already running! No one is safe from this style of error.

A safer alternative when you are trying to specify a specific target is tab completion. If you hit tab in the shell, it'll try to figure out what you're going to type and automatically complete it. Auto-completion is super useful, and this challenge will explore its use in specifying files.

This challenge has copied the flag into /challenge/pwncollege, and you can freely cat that file. But you can't type the filename: we used some serious trickery to make sure that you must tab-complete it. Try it out!

hacker@dojo:\~$ ls /challenge
DESCRIPTION.md  pwncollege
hacker@dojo:\~$ cat /challenge/pwncollege
cat: /challenge/pwncollege: No such file or directory
hacker@dojo:\~$ cat /challenge/pwn<TAB>
pwn.college{HECK YEAH}
hacker@dojo:\~$
When you hit that tab key, the name will expand and you'll be able to read the file. Good luck!

### Solve:
**Flag:** `pwn.college{QTSl_QtONPA9aofmkuPTd0Sh0Wo.0FN0EzNxwCN2gjNzEzW}`

I pressed the tab key to auto complete in the shell.
```
hacker@globbing~tab-completion:~$ cat /challenge/pwncollege​ 
pwn.college{QTSl_QtONPA9aofmkuPTd0Sh0Wo.0FN0EzNxwCN2gjNzEzW}
```

### New Learnings
I learnt that * can lead to errors and usage of unintended files. Tabbing is a better way to shorten typing.

### References

## Multiple options for tab completion
Consider the following situation:

hacker@dojo:\~$ ls
flag  flamingo  flowers
hacker@dojo:\~$ cat f<TAB>
There are multiple options! What happens?

What happens varies based on the specific shell and its options. By default bash will auto-expand until the first point when there are multiple options (in this case, fl). When you hit tab a second time, it'll print out those options. Other shells and configurations, instead, will cycle through the options.

This challenge has a /challenge/files directory with a bunch of files starting with pwncollege. Tab-complete from /challenge/files/p or so, and make your way to the flag!

