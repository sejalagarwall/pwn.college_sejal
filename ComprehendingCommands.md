# Comprehending Commands

## Cat: not the pet, but the command!
One of the most critical Linux commands is cat. cat is most often used for reading out files, like so:

hacker@dojo:\~$ cat /challenge/DESCRIPTION.md
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

## Catting absolute paths
In the last level, you did cat flag to read the flag out of your home directory! You can, of course, specify cat's arguments as absolute paths:

hacker@dojo:\~$ cat /challenge/DESCRIPTION.md
In the last level, you did `cat flag` to read the flag out of your home directory!
You can, of course, specify `cat`'s arguments as absolute paths:
...
In this directory, I will not copy it to your home directory, but I will make it readable. You can read it with cat at its absolute path: /flag.

### Solve
**Flag:** `pwn.college{g5iHxGWRq-rkuG0lqYqmGU3alHk.QX5ETO0wCN2gjNzEzW}`

I used cat to read the flag file by using its absolute path as an argument.
```
hacker@commands~catting-absolute-paths:~$ cat /flag
pwn.college{g5iHxGWRq-rkuG0lqYqmGU3alHk.QX5ETO0wCN2gjNzEzW}
```

### New Learnings
I learnt that you can use absolute paths to read files using cat.

### References

## More catting practice
You can specify all sorts of paths as arguments to commands, and we'll practice some more with cat. In this level, I'll put the flag in some crazy directory, and I will not allow you to change directories with cd, so no cat flag for you. You must retrieve the flag by absolute path, wherever it is.

### Solve
**Flag:** `pwn.college{MC6OfHUYAlX1mL4uBMi3PfXTR2Q.QXwITO0wCN2gjNzEzW}`

I used cat to read flag by copying the absolute path of the file.
```
hacker@commands~more-catting-practice:~$ cat /lib/x86_64-linux-gnu/gio/flag
pwn.college{MC6OfHUYAlX1mL4uBMi3PfXTR2Q.QXwITO0wCN2gjNzEzW}
```

### New Learnings
I got more clarity on absolute paths as arguments to cat.

### References

## Grepping for a needle in a haystack
Sometimes, the files that you might cat out are too big. Luckily, we have the grep command to search for the contents we need! We'll learn it in this challenge.

There are many ways to grep, and we'll learn one way here:

hacker@dojo:\~$ grep SEARCH_STRING /path/to/file
Invoked like this, grep will search the file for lines of text containing SEARCH_STRING and print them to the console.

In this challenge, I've put a hundred thousand lines of text into the /challenge/data.txt file. grep it for the flag!

HINT: The flag always starts with the text pwn.college.

### Solve
**Flag:** `pwn.college{0oGixMtdmO7ZuaMO24jgocsollS.QX3EDO0wCN2gjNzEzW}`

I used the grep command to search for 'pwn.college' as the flag always contains that keyword.
```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{0oGixMtdmO7ZuaMO24jgocsollS.QX3EDO0wCN2gjNzEzW}
```

### New Learnings
I learnt about the grep command and that it's used to search for strings in huge files where catting is not feasible.

### References

## Comparing files

When looking for changes between similar files, eyeballing them might not be the most efficient approach! This is where the diff command becomes invaluable.

diff compares two files line by line and shows you exactly what's different between them. For example:

hacker@dojo\:~$ cat file1
hello
world
hacker@dojo:\~$ cat file2
hello
universe
hacker@dojo:\~$ diff file1 file2
2c2
< world
\---
\> universe
The output tells us that line 2 changed (2c2), with world in the first file (<) being replaced by universe in the second file (>).

Sometimes, when new lines are added, you'll see something like:

hacker@dojo:\~$ cat old
pwn
hacker@dojo:\~$ cat new
pwn
college
hacker@dojo:\~$ diff old new
1a2
\> college
This tells us that after line 1 in the first file, the second file has an additional line (1a2 means "after line 1 of file1, add line 2 of file2").

Now for your challenge! There are two files in /challenge:

/challenge/decoys_only.txt contains 100 fake flags
/challenge/decoys_and_real.txt contains all 100 fake flags plus the one real flag
Use diff to find what's different between these files and get your flag!

### Solve
**Flag:** `pwn.college{MTWoEWSJxIh9asChH3ej5MXiPPS.01MwMDOxwCN2gjNzEzW}`

I used the diff command with the absolute paths of the two files I had to differentiate between to find the flag.
```
hacker@commands~comparing-files:~$ diff /challenge/decoys_only.txt /challenge/decoys_and_real.txt
98a99
> pwn.college{MTWoEWSJxIh9asChH3ej5MXiPPS.01MwMDOxwCN2gjNzEzW}
```

### New Learnings
I learnt about the diff commmand. It is used to differentiate between files. The format for the changed lines (1a2 for example)is new to me as well.

### References

## Listing files
