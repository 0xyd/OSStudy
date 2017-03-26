# OSStudy
An Open note for people who want to study OS.

# Outline

1. Chapter 1: Introduction
2. Chapter 2: System Structures
3. Chapter 3: Process Concept
4. Chapter 4: Multithreaded Programming
5. Chapter 5: Process Scheduling
6. Chapter 6: Synchronization
7. Chapter 7: Deadlocks
8. Chapter 8: Memory-Management Strategies
9. Chapter 9: Virtual-Memory Management
10. Chapter 10: File System
11. Chapter 11: Implementing File-Systems
12. Chapter 12: Mass-Storage Structure
13. Chapter 13: I/O Systems
14. Chapter 14: System Protection
15. Chapter 15: System Security
16. Chapter 16: The Linux System


# Chapter 1: Introduction

# Chapter 10: File System

## Secondary Storage

Because the memory is too small to store all our data, we need a bigger storage to put our data.

## File System

It is designed to allow users to manipulate the data or programs in the secondary storage.

File: A collection of related information with *logical interpretation* for users, creators or applications.

Directory Structure: 

## Access Methods for Files: 

1. Sequential Acceess:

Information in the file is processed inorder. Ex: Compiler or text editor.


2. Direct Access (Relative Access)

File is a numbered sequence of blocks (Fixed length of logical records). 
Use block number n to decide where to start read or write.


3. Index-Based Access

Directory: A symbol table that translates file names into their directory entries.


## Schemes of Directory's Logical Structure:

1. Single-Level Directory

All files contain in the same directory

2. Two-Level Directory

Every users has their own directories call **user file directory**.

All **use file directories** are under **master file directory**.


3. Tree-Structure Directory

There is a **root directory** where every path starts from and start the concept of **Absolute Path** and **Relative Path**.

There are many **subdirectories** beneath the root directory and each of them may have multiple levels.

Ex: DOS.

4. Acyclic-Graph Directory

Unlike Tree-Structure Directory, an Acyclic-Graph Directory allows files be shared. 

The way different directories share the files are links and they have two types.

One is symbolic link and another one is hard link. 

However, Acyclic-Graph has to assure that there is no cycles in the structure,

It does not allow users to use hard links to link a directory because Acyclic-Graph Directory's algorithm can not identify between hard link and directory.

Thus, it causes an infinite loop. Although the symbolic links are allowed to link directory, the traverse algorithm can identify the softlink and avoid to access it.


5. General Graphic Directory

All kinds of scheme are General Graphic Directory, including those allow the infinite loops existing in directory.

## Hard Link and Symbolic Link

Hard Link: Directory entry creates a link that point to the i-node that describes the content directly.

Symbolic Link: Also named soft link, is implemented as a file has its own i-node which contains the path the link points to.

The size of a symbolic link is the same as the pathname. 

Ex: Shortcut in Windows system.

## File System Mounting

**Mounting** is an action must be made before starting to access the disk.

**Mounting point** is the place an unmounted system to be mount. 

# Chapter 11: Implementing File-Systems



# Chapter 12: Mass-Storage Structure

# Chapter 13: I/O Systems

# Chapter 14: System Protection

# Chapter 15: System Security

# Chapter 16: The Linux System

# Reference

* [Operating System Concepts 9th edition ](http://as.wiley.com/WileyCDA/WileyTitle/productCd-EHEP002013.html)
* [Wikipedia](https://www.wikipedia.org)

