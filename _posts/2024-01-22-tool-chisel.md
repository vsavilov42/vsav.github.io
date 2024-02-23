---
layout: single
title: Chisel -- Tool Portforwarding
date: 2024-02-20
classes: wide
header:
    icon: /assets/images/toolChisel/HeadChisel.PNG
categories:
  - Tool
  - SSH
tags:
  - Tool
  - Linux
  - Windows
  - SSH
---

This post is for explain chisel in his basic state, used to create a server and client to allow portforwarding between two machines.

Tool: [Chisel Github](https://github.com/jpillora/chisel "Chisel github by jpillora")

## Concept of Chisel Client-Server
![](/assets/images/Tool-Chisel/WorkflowClient-server.PNG)

## Commands for Windows and Linux

```
Server: chisel server -reverse -port [PortNum]

Client: chisel [AttackerIP]:[PortNum] [VictimIP/Loopback]:[PortNumVictim]
```

## Example

PoC: Linux IP: 10.0.2.10
     Windows IP: 10.0.3.10

```
Linux machine command: ./chisel server -reverse -port 8888
Windows machine command: chisel.exe client 10.0.2.10:8888 127.0.0.1:443
```