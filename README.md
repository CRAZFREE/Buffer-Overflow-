# Secure System Engineering - Assignment 2

**Course:** IITM-CS5691  
**Student:** Sambhav Jain  
**Roll No:** CS23M060  
**Date:** August 2024

## Overview

This repository contains the solution for Assignment 2 of the Secure System Engineering course at IIT Madras. The assignment focuses on identifying and exploiting vulnerabilities in a provided C code, particularly targeting buffer overflow attacks, fixed canary values, and inactive Address Space Layout Randomization (ASLR).

## Problem Statement

The task is to analyze the provided C code (`assignment_2.c`) and identify any existing security vulnerabilities. Specifically, we need to explore the potential for buffer overflow attacks, the implications of fixed canary values, and the absence of ASLR. The objective is to demonstrate how these vulnerabilities can be exploited, particularly using a return-to-libc attack, and to suggest possible mitigations.

## Vulnerabilities Identified

### 1. Buffer Overflow
- **Description**: The code is vulnerable to buffer overflow attacks, where an attacker can overwrite the return address on the stack, redirecting execution flow to malicious code.
- **Impact**: Allows arbitrary code execution, potentially leading to unauthorized access or control over the system.

### 2. Fixed Canary Value
- **Description**: The stack canary, intended to detect buffer overflows, is fixed and does not change between program executions. This predictability makes it vulnerable to systematic overwriting.
- **Impact**: Enables an attacker to bypass the canary protection and manipulate the stack, leading to successful exploitation.

### 3. Inactive ASLR (Address Space Layout Randomization)
- **Description**: ASLR, a security feature that randomizes memory addresses, is not enabled. As a result, crucial memory addresses remain static across executions.
- **Impact**: Simplifies the process of crafting exploits like return-to-libc, as the memory addresses of system functions and strings like `/bin/sh` remain predictable.

## Exploit Strategy: Return-to-Libc Attack

Given the vulnerabilities identified, the most suitable attack for executing arbitrary code is the return-to-libc attack. This attack leverages the predictable memory addresses (due to inactive ASLR) and the ability to overwrite the return address (due to buffer overflow) to redirect program execution to a system call that opens a shell.

### Steps to Execute the Attack

1. **Buffer Overflow**: Overflow the buffer to overwrite the return address on the stack.
2. **Canary Overwrite**: Exploit the fixed canary value to avoid detection.
3. **Return Address Manipulation**: Replace the original return address with the address of the `system` function.
4. **Argument Setup**: Provide `/bin/sh` as an argument to the `system` call, which opens a shell.

## Directory Structure

```plaintext
SecureSystemEngineering_Assignment2/
├── README.md
├── source_code/
│   ├── source_code.c       # Vulnerable C code
│   ├── exploit.c            # Exploit code demonstrating the attack
├── docs/
│   ├── report.pdf           # Detailed report on the vulnerabilities and exploit
├── .gitignore
├── LICENSE                  # License file (optional)
