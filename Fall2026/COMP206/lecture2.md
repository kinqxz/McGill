# COMP 206 — Lecture 2

**Course:** Introduction to Software Systems  
**Date:** September 3rd 2026
**Topic:** Linux

---

## Learning goals
After this lecture, you will:
- Be familiar with the basic computer hardware components
- Be familiar with Operating Systems and their purpose
- Be familiar with the history of Unix and Linux
- Know the structure of the Linux File System (Including the differnece between absolute vs relative values)
- Have seen basic file manipulation on the Linux command line

## Main Computer Hardware Components
- Storage (disk): holds data at rest
- Memory (RAM): holds data that is live
- Processor (CPU): performs computations

## Operating system
- "Insulates" applications running on a computer, both from the hardware of that computer and also from each other.
- "Insulates" the user from the coplex inner workings of the computer
- OS is itself a system! Components include: the kernel, the network stack, the filesystem, a hardware abstraction layer.
- OS provides programmers with system librarires to perfom OS-level operations, e.g. using network connections, allocating memory, managing files, using peripherals (Bluetooth, USB, etc.)
- Primary function of the OS: managing the computer's resources.

## Linux
- A family of free and open-source operating systems (called Linux distributions) based on the Linux kernel
  - Kernel: performs core OS functions. Includes: networking, filesystem, user accounts/permissions, memory management, device drivers, and even more.
  - OS Components that are not part of the kernel include the user interface (shell, GUI), the utilities the bootloader, etc.
- Most distributions are based on a combination of the Linux kernel and utilities from the GNU Project:
  - Ubuntu, Devian, CentOs....
  - Other distributions not based on GNU include Android and ChromeOS

## File System (FS)
Underlying concept: Tree data structure
- Node vs leaf
- Data stored in nodes
- Distinguished node: the root

Hierarchical file system:
Two different kind of entries in this tree:
- Directories:
  - Structural. Contents is dirs or files. Also called folders.
- Files:
  - Content is data, e.g. documents, programs, etc. File system doesn't distinguish between files

Intuition: How to refer to a location in space?
- Absolute approach, the full address:
  - Full adress, doesn't depend on the current location
- Relative approach, directions from "here":
  - Down the hall, on the left
  - Depends on current location: this doesn't work if you're saying this from another building.

Absolute path ex.: /etc/network/interface
Relative path ex.: ../etc/network/interfaces

## Some commands that will be seen in Lecture 3
- Using **touch** to create a file
- Using **mkdir** to make a directory
- Using **rm** to remove a file
  - And **rm -r** to remove a directory
- Using **mv** to move a file/directory
- Using **cp** to copy a file
  - And **cp -r** to copy a directory