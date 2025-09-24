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
**FLag:** `pwn.college{0oGixMtdmO7ZuaMO24jgocsollS.QX3EDO0wCN2gjNzEzW}`

I used the grep command to search for 'pwn.college' as the flag always contains that keyword.
```
hacker@commands~grepping-for-a-needle-in-a-haystack:~$ grep pwn.college /challenge/data.txt
pwn.college{0oGixMtdmO7ZuaMO24jgocsollS.QX3EDO0wCN2gjNzEzW}
```

### New Learnings
I learnt about the grep command and that it's used to search for strings in huge files where catting is not feasible.

### References

## 
