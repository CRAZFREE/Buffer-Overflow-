The certain C code assignment_2 has certain vulnerabilities, one is buffer overflow
through which we can modify the return address and rewrite the return address to our own
exploit code. Along with that there is return to libc attack possible. We can manipulate the
stack , altering the return address of a function and redirecting the flow to execute the code
which we want.The goal is to execute the shell, by providing the ¨/bin/sh" as an argument.


Files provided
• Makefile
• assignment_2.c
• assignment_2 (binary) [ sha256sum:12407ba5f5dc90974e008d8e2b46aaa9d1a38e3a3c95e5d634925fb712551542 ]
• This README

