# Terminal Multiplexing

## Launching screen
Let's dive right in!

screen is a program that creates virtual terminals inside your terminal. It's somewhat like having multiple browser tabs, but for your command line!

Starting screen is super simple:
```
hacker@dojo:~$ screen
```
That's it! You're now inside a screen session. It looks exactly like a terminal, but there are new capabilities there, waiting to be discovered.

For this challenge, we've hooked things up so that just launching screen will get you the flag. Easy!

### Solve
**Flag:** `pwn.college{kbE88i89zl9E65RoxqLEGWIAoG8.0VN4IDOxwCN2gjNzEzW}`

I opened a screen using the screen command and exited by typing exit.
```
hacker@terminal-multiplexing~launching-screen:~$ screen
[screen is terminating]

Congratulations! You're inside a screen session!
Here's your flag:
pwn.college{kbE88i89zl9E65RoxqLEGWIAoG8.0VN4IDOxwCN2gjNzEzW}
```

### New Learnings
I learnt about terminals inside terminals and how to open one using the screen command.

### References

## Detaching and attaching
Now we'll start digging in with the magic of detaching!

Imagine you're working on something important over a remote connection, and your connection drops. With a normal terminal (outside of this awesome dojo environment), everything's gone. With screen, your work keeps running, and you can reattach later!

You can also detach on purpose, which we'll do in this challenge. You detach by pressing Ctrl-A, followed by d (for detach). This leaves your session running in the background while you return to your normal terminal.
```
hacker@dojo:~$ screen
[doing some work...]
[Press Ctrl-A, then d]
[detached from 12345.pts-0.hostname]
hacker@dojo:~$
```
To reattach, you can use the -r argument to screen:
```
hacker@dojo:~$ screen -r
```
For this challenge, you'll need to:

Launch screen
Detach from it.
Run /challenge/run (this will secretly send the flag to your detached session!)
Reattach to see your prize

### Solve
**Flag:** `pwn.college{0_0JejSqCGGChE3YzqSJhcYqMe-.0lN4IDOxwCN2gjNzEzW}`

I went into the screen, detatched and ran /challenge/run. Reattached and got the flag.
```
hacker@terminal-multiplexing~detaching-and-attaching:~$ screen
[detached from 140.pts-0.terminal-multiplexing~detaching-and-attaching]
hacker@terminal-multiplexing~detaching-and-attaching:~$ /challenge/run
Found detached screen session: 140.pts-0.terminal-multiplexing~detaching-and-attaching
Sending flag to your screen session...

Flag sent! Now reattach to your screen session with:

  screen -r

You'll find the flag waiting for you there!
hacker@terminal-multiplexing~detaching-and-attaching:~$ screen -r
[screen is terminating]

hacker@terminal-multiplexing~detaching-and-attaching:~$
hacker@terminal-multiplexing~detaching-and-attaching:~$ echo Yes! Flag is: pwn.college{0_0JejSqCGGChE3YzqSJhcYqMe-.0lN4IDOxwCN2gjNzEzW}
Yes! Flag is: pwn.college{0_0JejSqCGGChE3YzqSJhcYqMe-.0lN4IDOxwCN2gjNzEzW}
```

### New Learnings
I learnt how to detach and reattach the screen.

### References

## Finding sessions
Time for some screen detective work!

If you become an avid screen user, you will inevitably end up with multiple sessions running. How do you find the right one to reattach to?

Well, we can list them:
```
hacker@dojo:~$ screen -ls
There are screens on:
        23847.mysession   (Detached)
        23851.goodwork    (Detached)
        23855.morework    (Detached)
3 Sockets in /run/screen/S-hacker.
```
The identifiers of the sessions are the PID of each respective screen process, a dot, and the name of the screen session. To attach to a specific one, you use its name or its PID by giving it as an argument to screen -r.
```
hacker@dojo:~$ screen -r goodwork
```
In this challenge, we've created three screen sessions for you. One of them contains the flag. The other two are decoys!

You'll need to check each one until you find it. Don't forget to detach (Ctrl-A d) before trying the next session!

### Solve
**Flag:** `pwn.college{Qx3vkFlR5l7kiQBEPzZqJkxUKM9.01N4IDOxwCN2gjNzEzW}`

I used -ls to list the screens and reattached to 2 screens before I found the flag.
```
hacker@terminal-multiplexing~finding-sessions:~$ screen -ls
There are screens on:
        144.session_d78f2148bb996dfb    (Detached)
        147.session_43b1701bf3793b7d    (Detached)
        150.session_b3eba8b8c491d374    (Detached)
3 Sockets in /home/hacker/.screen.
hacker@terminal-multiplexing~finding-sessions:~$ screen -r 144
[detached from 144.session_d78f2148bb996dfb]
hacker@terminal-multiplexing~finding-sessions:~$ screen -r 147
[screen is terminating]

hacker@terminal-multiplexing~finding-sessions:~$  echo 'Congratulations! You found the right session!'
Congratulations! You found the right session!
hacker@terminal-multiplexing~finding-sessions:~$  echo pwn.college{Qx3vkFlR5l7kiQBEPzZqJkxUKM9.01N4IDOxwCN2gjNzEzW}
pwn.college{Qx3vkFlR5l7kiQBEPzZqJkxUKM9.01N4IDOxwCN2gjNzEzW}
```

### New Learnings
I learnt about listing screens and using their PID or name to go into a specific screen.

### References

## Switching windows
Okay, so far, screen is just a weird sort of terminal-with-a-terminal. But it can be much more!

Inside a single screen session, you can have multiple windows, like your browser has multiple tabs. This can be super handy for organizing different tasks!

These windows are handled with different keyboard shortcuts, all starting with Ctrl-A:

Ctrl-A c - Create a new window
Ctrl-A n - Next window
Ctrl-A p - Previous window
Ctrl-A 0 through Ctrl-A 9 - Jump directly to window 0-9
Ctrl-A " - bring up a selection menu of all of the windows
For this challenge, we've set up a screen session with two windows:

Window 0 has... well, you'll have to switch there to find out!
Window 1 has a welcome message
Attach to the session with screen -r, then use one of the key combinations above to switch to Window 1. Go get that flag!

### Solve
**Flag:** `pwn.college{sd3IzAlTb745-iGGFsvsUgIqtbq.0FO4IDOxwCN2gjNzEzW}`

I used screen -r to open a screen and Ctrl-A 0 to switch to window 0 for the flag.
```
hacker@terminal-multiplexing~switching-windows:~$ screen -r
[detached from 135.challenge_session]

hacker@terminal-multiplexing~switching-windows:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{sd3IzAlTb745-iGGFsvsUgIqtbq.0FO4IDOxwCN2gjNzEzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{sd3IzAlTb745-iGGFsvsUgIqtbq.0FO4IDOxwCN2gjNzEzW}
```

### New Learnings
I learnt how to pull up different windows inside a screen. I also learnt about different commands.

### References

## Detaching and attaching (tmux)
Let's try the same thing with tmux!

tmux (terminal multiplexer) is screen's younger, more modern cousin. It does all the same things but with some different key bindings. The biggest difference? Instead of Ctrl-A, tmux uses Ctrl-B as its command prefix.

So to detach from tmux, you press Ctrl-B followed by d.
```
hacker@dojo:~$ tmux
[doing some work...]
[Press Ctrl-B, then d]
[detached (from session 0)]
hacker@dojo:~$
```
The commands also differ:

tmux ls - List sessions
tmux attach or tmux a - Reattach to session
For this challenge:

Launch tmux
Detach from it.
Run /challenge/run (this will send the flag to your detached session!)
Reattach to see your prize

### Solve
**Flag:** `pwn.college{Q5RsOuknKu4eSLFj3Omre2k61yn.0VO4IDOxwCN2gjNzEzW}`

I used tmux to open a screen, detached, ran /challenge/run and reattached to get the flag.
```
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ tmux
[detached (from session 0)]
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ /challenge/run
Found detached tmux session: 0
Sending flag to your tmux session...

Flag sent! Now reattach to your tmux session with:
  tmux attach

You'll find the flag waiting for you there!
hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$ tmux a

hacker@terminal-multiplexing~detaching-and-attaching-tmux:~$  echo Congratulations, here is your flag: pwn.college{Q5RsOuknKu4eSLFj3Omre2k61yn.0VO4IDOxwCN2gjNzEzW}
Congratulations, here is your flag: pwn.college{Q5RsOuknKu4eSLFj3Omre2k61yn.0VO4IDOxwCN2gjNzEzW}
```

### New Learnings
I learnt how to use tmux to use and manipulate screens.

### References

## Switching windows (tmux)
Let's learn to navigate windows in tmux!

Just like screen, tmux has windows. The key combos are different, but the concept is the same:

Ctrl-B c - Create a new window
Ctrl-B n - Next window
Ctrl-B p - Previous window
Ctrl-B 0 through Ctrl-B 9 - Jump to window 0-9
Ctrl-B w - See a nice window picker
Tmux shows your windows at the bottom in a status bar that looks like:
```
[0] 0:bash* 1:bash
```
The * shows your current window, and each entry also shows the process that the window was created to run.

We've created a tmux session with two windows:

Window 0 has the flag!
Window 1 has your warm welcome.
Go get that flag!

### Solve
**Flag:** `pwn.college{IS6p5cgS1T83wARIFAOnsOx5RVB.0FM5IDOxwCN2gjNzEzW}`

I used tmux to open a screen. I used Ctrl-B w to look through the windows and open the one containing the flag.
```
hacker@terminal-multiplexing~switching-windows-tmux:~$ tmux
[detached (from session challenge_session)]

hacker@terminal-multiplexing~switching-windows-tmux:~$  cat <<MSG
> Excellent work! You found window 0!
> Here is your flag: pwn.college{IS6p5cgS1T83wARIFAOnsOx5RVB.0FM5IDOxwCN2gjNzEzW}
> MSG
Excellent work! You found window 0!
Here is your flag: pwn.college{IS6p5cgS1T83wARIFAOnsOx5RVB.0FM5IDOxwCN2gjNzEzW}
```

### New Learnings
I learnt about additional commands in tmux.

### References
