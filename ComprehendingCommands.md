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
So far, we've told you which files to interact with. But directories can have lots of files (and other directories) inside them, and we won't always be here to tell you their names. You'll need to learn to list their contents using the ls command!

ls will list files in all the directories provided to it as arguments, and in the current directory if no arguments are provided. Observe:

hacker@dojo:\~$ ls /challenge
run
hacker@dojo:\~$ ls
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:\~$ ls /home/hacker
Desktop    Downloads  Pictures  Templates
Documents  Music      Public    Videos
hacker@dojo:\~$
In this challenge, we've named /challenge/run with some random name! List the files in /challenge to find it.

### Solve
**Flag:** `pwn.college{AmEgUshjK4XI-lkJwFqH3tDdj3N.QX4IDO0wCN2gjNzEzW}`

I listed the files in /challenge and found the file to be runned and then I called the file to get the flag.
```
hacker@commands~listing-files:~$ ls /challenge
3853-renamed-run-12236  DESCRIPTION.md
hacker@commands~listing-files:~$ /challenge/3853-renamed-run-12236
Yahaha, you found me! Here is your flag:
pwn.college{AmEgUshjK4XI-lkJwFqH3tDdj3N.QX4IDO0wCN2gjNzEzW}
```

### New Learnings
I learnt about the ls command and how it is used to list all files in a directory. 

### References

## Touching files
Of course, you can also create files! There are several ways to do this, but we'll look at a simple command here. You can create a new, blank file by touching it with the touch command:

hacker@dojo:\~$ cd /tmp
hacker@dojo:/tmp$ ls
hacker@dojo:/tmp$ touch pwnfile
hacker@dojo:/tmp$ ls
pwnfile
hacker@dojo:/tmp$
It's that simple! In this level, please create two files: /tmp/pwn and /tmp/college, and run /challenge/run to get your flag!

### Solve
**Flag:** `pwn.college{8EIdT7DDwsHMApJwIyN_zKmzQGU.QXwMDO0wCN2gjNzEzW}`

I changed directories to create the files in /tmp. I used touch command to create the two files and ls command to check if they have been created. 
```
hacker@commands~touching-files:~$ cd /tmp
hacker@commands~touching-files:/tmp$ touch pwn
hacker@commands~touching-files:/tmp$ touch college
hacker@commands~touching-files:/tmp$ ls
bin  college  hsperfdata_root  pwn  tmp.TpSOPGOVKK
hacker@commands~touching-files:/tmp$ /challenge/run
Success! Here is your flag:
pwn.college{8EIdT7DDwsHMApJwIyN_zKmzQGU.QXwMDO0wCN2gjNzEzW}
```

### New Learnings
The touch command is used to create new files in a directory. You have to be in the specific directory you want to create the file in.

### References

## Removing files
Files are all around you. Like candy wrappers, there'll eventually be too many of them. In this level, we'll learn to clean up!

In Linux, you remove files with the rm command, as so:

hacker@dojo:\~$ touch PWN
hacker@dojo:\~$ touch COLLEGE
hacker@dojo:\~$ ls
COLLEGE     PWN
hacker@dojo:\~$ rm PWN
hacker@dojo:\~$ ls
COLLEGE
hacker@dojo:\~$
Let's practice. This challenge will create a delete_me file in your home directory! Delete it, then run /challenge/check, which will make sure you've deleted it and then give you the flag!

### Solve
**Flag:** `pwn.college{MH11HgKnz8PTFjeHFmVhTzgzdJK.QX2kDM1wCN2gjNzEzW}`

I deleted a file using the rm command.
```
hacker@commands~removing-files:~$ rm delete_me
hacker@commands~removing-files:~$ /challenge/check
Excellent removal. Here is your reward:
pwn.college{MH11HgKnz8PTFjeHFmVhTzgzdJK.QX2kDM1wCN2gjNzEzW}
```

### New Learnings
I got to know about the rm command to delete files. I also tested it around by being in a different directory and learnt that you need to be in the directory you are deleting files from.

### References

## Moving files
You can also move files around with the mv command. The usage is simple:

hacker@dojo:\~$ ls
my-file
hacker@dojo:\~$ cat my-file
PWN!
hacker@dojo:\~$ mv my-file your-file
hacker@dojo:\~$ ls
your-file
hacker@dojo:\~$ cat your-file
PWN!
hacker@dojo:\~$
This challenge wants you to move the /flag file into /tmp/hack-the-planet (do it)! When you're done, run /challenge/check, which will check things out and give the flag to you.

### Solve
**Flag:** `pwn.college{0bu9Q-D-U55iBulY8LIpOo6fOez.0VOxEzNxwCN2gjNzEzW}`

I used the mv command to move the file to a different directory. I initially thought you had to be in the /tmp directory to move the file to /tmp/..., however you can move files using their absolute paths.
```
hacker@commands~moving-files:~$ mv /flag /tmp/hack-the-planet
Correct! Performing 'mv /flag /tmp/hack-the-planet'.
hacker@commands~moving-files:~$ /challenge/check
Congrats! You successfully moved the flag to /tmp/hack-the-planet! Here it is:
pwn.college{0bu9Q-D-U55iBulY8LIpOo6fOez.0VOxEzNxwCN2gjNzEzW}
```

### New Learnings
You can use the mv command to move and rename files. 

### References

## 
