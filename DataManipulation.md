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
Here, the backslash (\\) signifies that the character that follows it is a standin for a character that's hard to input into the shell normally. The newline, of course, is hard to input because when you typically hit Enter, you'll run the command itself. \n is a standin for this newline, and it must be in quotes to prevent the shell interpreter itself from trying to interpret it and pass it to tr instead.

Now, let's combine this with deletion. In this challenge, we'll inject a bunch of newlines into the flag. Delete them with tr's -d flag and the escaped newline specification!

Fun fact! Want to actually replace a backslash (\\) character? Because \\ is the escape character, you gotta escape it! \\\\ will be treated as a backslash by tr. This isn't relevant to this challenge, but is a fun fact nonetheless!

### Solve
**Flag:** `pwn.college{cPDHRMHq-qp4zRjIvgN320PmV_d.0VNxEzNxwCN2gjNzEzW}`

I deleted newlines from the flag by using "\n" as an argument to the tr command.
```
hacker@data~deleting-newlines:~$ /challenge/run | tr -d "\n"
Your line-split flag: pwn.college{cPDHRMHq-qp4zRjIvgN320PmV_d.0VNxEzNxwCN2gjNzEzW}
```

### New Learnings
I learnt about deleting newlines and how it's important to use quotes around them.

### References

## Extracting the first lines with head
In your Linux journey, you'll experience situations where you need to grab just the early output of very verbose programs. For this, you'll reach for head! The head command is used to display the first few lines of its input:

hacker@dojo:\~$ cat /something/very/long | head
this
is
just
the
first
ten
lines
of
the
file
hacker@dojo:\~$
By default, it shows the first 10 lines, but you can control this with the -n option:

hacker@dojo:\~$ cat /something/very/long | head -n 2
this
is
hacker@dojo:\~$
This challenge's /challenge/pwn outputs a bunch of data, and you'll need to pipe it through head to grab just the first 7 lines and then pipe them onwards to /challenge/college, which will give you the flag if you do this right! Your solution will be a long composite command with two pipes connecting three commands. Good luck!

### Solve
**Flag:** `pwn.college{UoFr2GCEjgRPYYMYJwjtjN17JT8.0lNxEzNxwCN2gjNzEzW}`

I used the head command to only pipe the first 7 lines as input to /challenge/college. I used two pipes to do this.
```
hacker@data~extracting-the-first-lines-with-head:~$ /challenge/pwn | head -n 7 | /challenge/college
Congratulations, you piped the right codes!
pwn.college{UoFr2GCEjgRPYYMYJwjtjN17JT8.0lNxEzNxwCN2gjNzEzW}
```

### New Learnings
I learnt about the head command and the -n argument.

### References

## Extracting specific sections of text
Sometimes, you want to grab specific columns of data, such as the first column, the third column, or the 42nd column. For this, there's the cut command.

For example, imagine that you have the following data file:

hacker@dojo:\~$ cat scores.txt
hacker 78 99 67
root 92 43 89
hacker@dojo:~$
You could use cut to extract specific columns:

hacker@dojo:\~$ cut -d " " -f 1 scores.txt
hacker
root
hacker@dojo:\~$ cut -d " " -f 2 scores.txt
78
92
hacker@dojo:\~$ cut -d " " -f 3 scores.txt
99
43
hacker@dojo:\~$
The -d argument specifies the column delimiter (how columns are separated). In this case, it's a space character. Of course, it has to be in quotes here so that the shell knows that the space is an argument rather than a space separating other arguments! The -f argument specifies the field number (which column to extract).

In this challenge, the /challenge/run program will give you a bunch of lines with random numbers and single characters (characters of the flag) as columns. Use cut to extract the flag characters, then pipe them to tr -d "\\n" (like the previous level!) to join them together into a single line. Your solution will look something like /challenge/run | cut ??? | tr ???, with the ??? filled out.

### Solve
**Flag:** `pwn.college{QMGzhW1XqZb5flL5aqb7_gntc2H.01NxEzNxwCN2gjNzEzW}`

I first ran the /challenge/run command to see which columns the flag was present in. Then I used the cut command to seperate the characters in flag from the other columns. I used piping to pipe the characters to tr where I deleted the nextlines to join the flag in one single line.
```
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run
866 p
6668 w
12700 n
13020 .
17895 c
19539 o
1198 l
30324 l
19859 e
3343 g
24767 e
20568 {
21633 Q
4235 M
9932 G
17173 z
15931 h
7385 W
6136 1
9189 X
8489 q
17145 Z
32752 b
3992 5
31386 f
19431 l
14378 L
31933 5
5888 a
4476 q
29955 b
12096 7
5762 _
22045 g
5544 n
32347 t
5255 c
21717 2
10164 H
9555 .
28920 0
21997 1
17505 N
30747 x
19640 E
22533 z
24163 N
28486 x
2019 w
21939 C
23260 N
12825 2
10766 g
15954 j
8456 N
20228 z
15108 E
6477 z
5774 W
29338 }
hacker@data~extracting-specific-sections-of-text:~$ /challenge/run | cut -d " " -f 
2 | tr -d "\n"
pwn.college{QMGzhW1XqZb5flL5aqb7_gntc2H.01NxEzNxwCN2gjNzEzW}
```

### New Learnings
I learnt how to cut out columns from outputs.

### References

## 
