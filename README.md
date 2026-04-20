# C and C++ Developer Toolkit for Microsoft Visual Studio Code using gcc compiler


Read the [How-To-Configure-VSC-C-CPP](./How-To-Configure-VSC-C-CPP.md) document.

Be sure to have [Visual Studio Code](https://code.visualstudio.com) installed.




## WSL GDB Error
Breakpoint 1 at 0x127c: file p4.c, line 11.
(gdb) run
Starting program: /home/<user>/ostep-code/cpu-api/p4
`warning: opening /proc/PID/mem file for lwp 1347.1347 failed: No such file or directory (2)`
Warning:
Cannot insert breakpoint 1.
Cannot access memory at address 0x8001269


### Check you WSL version
PS> wsl --version

E.g.
WSL version: 2.6.3.0
Kernel version: 6.6.87.2-1

### See if there's an update
PS> wsl --update


### GDB Error
It usually stems from a security feature in the Linux kernel called ptrace_scope, or a mismatch in how WSL handles memory access to /proc

### Temp Disable ptrace_scope restrictions

Bash> echo 0 | sudo tee /proc/sys/kernel/yama/ptrace_scope
    - 0: Classic ptrace permissions (GDB can attach to processes).
    - 1: Restricted ptrace (Default on many systems).

### restart WSL
PS> wsl --shutdown

### Permanent setting `ptrace_scope`
/etc/sysctl.d/10-ptrace.conf and setting kernel.yama.ptrace_scope = 0