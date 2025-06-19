---
layout:     post
title:      "Exception and Interrupt"
date:       2024-04-15 21:40:00
author:     "Bing"
catalog:    true
tags:
    - CPU
    - Computer
    - RISC-V
---

Take RISC-V as example.

# CPU Interrupt Support
Registers:
* mip / sip
* mie / sie
* topi / topei

Hardware unit:
* APLIC
* IMSIC

## IPI (Interprocessor Interrupt)

# IRQ (Interrupt Request)

# Kernel handling
## Configuration
```
cat /proc/interrupts
```