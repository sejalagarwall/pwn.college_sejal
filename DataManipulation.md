# Data Manipulation

## Translating characters
One of the purposes of piping data is to modify it. Many Linux commands will help you modify data in really cool ways. One of these is tr, which translates characters it receives over standard input and prints them to standard output.

In its most basic usage, tr translates the character provided in its first argument to the character provided in its second argument:

hacker@dojo:\~$ echo OWN | tr O P
PWN
hacker@dojo:\~$
It can also handle multiple characters, with the characters in different positions of the first argument replaced with associated characters in the second argument.

hacker@dojo:\~$ echo PWM.COLLAGE | tr MA NE
PWN.COLLEGE
hacker@dojo:\~$
Now, you try it! In this level, /challenge/run will print the flag but will swap the casing of all characters (e.g., A will become a and vice-versa). Can you undo it with tr and get the flag?

### Solve
**Flag:** `pwn.college{YaSGxecAoOOvL432STc2ZvJvMpL.01MxEzNxwCN2gjNzEzW}`

I entered all the alphabets twice in different cases so that the case switch happens.
```
hacker@data~translating-characters:~$ /challenge/run | tr AaBbCcDdEeFfGgHhIiJjKkLlM
mNnOoPpQqRrSsTtUuVvWwXxYyZz aAbBcCdDeEfFgGhHiIjJkKlLmMnNoOpPqQrRsStTuUvVwWxXyYzZ
yOUR CASE-SWAPPED FLAG:
pwn.college{YaSGxecAoOOvL432STc2ZvJvMpL.01MxEzNxwCN2gjNzEzW}
```

### New Learnings
I learnt about the tr command and how it's used to replace letters.

### References

## Deleting characters
tr can also translate characters to nothing (i.e., delete them). This is done via a -d flag and an argument of what characters to delete:

hacker@dojo:\~$ echo PAWN | tr -d A
PWN
hacker@dojo:\~$
Pretty simple! Now you give it a try. I'll intersperse some decoy characters (specifically: ^ and %) among the flag characters. Use tr -d to remove them!

### Solve
**Flag:** `pwn.college{MN3EEzLXa6YmvHValAWQu0WiDte.0FNxEzNxwCN2gjNzEzW}`

I used the -d argument to remove ^ and % from the flag.
```
hacker@data~deleting-characters:~$ /challenge/run | tr -d %^
Your character-stuffed flag:
pwn.college{MN3EEzLXa6YmvHValAWQu0WiDte.0FNxEzNxwCN2gjNzEzW}
```

### New Learnings
I learnt how to delete characters from an output.

### References

## Deleting newlines
A common class of characters to remove is a line separator. This happens when you have a stream of data that you want to turn into a single line for further processing. You can specify newlines almost like any other character, by escaping them:

hacker@dojo:\~$ echo "hello_world!" | tr _ "\n"
hello
world!
hacker@dojo:\~$
Here, the backslash (\) signifies that the character that follows it is a standin for a character that's hard to input into the shell normally. The newline, of course, is hard to input because when you typically hit Enter, you'll run the command itself. \n is a standin for this newline, and it must be in quotes to prevent the shell interpreter itself from trying to interpret it and pass it to tr instead.

Now, let's combine this with deletion. In this challenge, we'll inject a bunch of newlines into the flag. Delete them with tr's -d flag and the escaped newline specification!

Fun fact! Want to actually replace a backslash (\) character? Because \ is the escape character, you gotta escape it! \\ will be treated as a backslash by tr. This isn't relevant to this challenge, but is a fun fact nonetheless!

