Level 06
===

In this tutorial, we are going to debug a program while exploiting it with PoE. To do it, we will use the gdb dynamic debugger.

### Overview

When writing the exploit, we will use the `pid()` function to get the process id 
of the exploited program. By placing `pause()` instructions in line with break-
points, we will be able to read process memory while debugging the target.

### Attaching to the target

On the first hand, we will begin by outputing the `pid` in the `act`:

```
act debug_act():
  dbgascii itoa(pid())
  pause()

submit:
  return debug_act()
```

On the second hand, we will run gdb and attach to the running process:
```
gdb 
(gdb) attach <pid>
Attaching to process <pid>
(gdb) info functions 
0x0000000100000000  _mh_execute_header
0x0000000100003e70  vuln
0x0000000100003f00  main
...
```

### Chosing your breakpoints

When chosing your breakpoints you will have to interupt the PoE script at some 
points, to avoid it to continue and terminate. To do it, place your `pause()`
instructions where you will set your breakpoints.