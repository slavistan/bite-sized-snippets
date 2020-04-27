---
title: Perform an action when a process' output matches a filter.
tags: zsh
---

```sh
# Create a named pipe
mkfifo fifo

# Mockup of a process whose output we're analyzing line by line. The process
# writes to our named pipe
{
sleep 5
echo "match" # here's what we're looking for
sleep 1000
} > fifo &

# Read from the fifo and pipe into `grep q' which blocks until a match is found.
( cat fifo & ) | grep -q 'match'

echo "<your action here>"
```

**Notes**

`cat fifo | grep -q 'match'` will not work because *cat* will not return until
the pipe is closed which might never happen for persistent processes causing
the whole pipeline to block indefinitely.

After grep returns the background process spawned by `( cat fifo & )` is
automatically terminated (cat receives a SIGPIPE).

`cat fifo` is to be preferred over `tail -f fifo` due to the fact, that *tail
may buffer the input before it flushes* into grep which will delay the action
either until the internal buffer is full or the process terminates. *cat
flushes each line immediately upon reception*.
