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

Directory: A symbol table that translates file names into their directory entries.

Directory Structure: 


## Access Methods for Files: 

1. Sequential Acceess:

Information in the file is processed inorder. Ex: Compiler or text editor.


2. Direct Access (Relative Access)

File is a numbered sequence of blocks (Fixed length of logical records). 
Use block number n to decide where to start read or write.


3. Index-Based Access




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

## File-System Structure

From the top to down: 

Application Programs --> Logical File System --> File-Organisation Module --> Basic file system --> I/O Control --> Devices

**Logical File System** manages Metadata which includes all of the file-system structure except the actual content(dir and data block). 
It maintains the file structure through **file control block** (Called i-node on Unix) and are also responsible for data protection.

**File-Organisation Module** maps logical block numbers (which i-node provides) to physical block numbers. Besides, it manages **free space** and is implemented with different types of **disk allocation**.

**Basic File System** translates generic commands for device drivers(Firmware).

**I/O Control** are the compositions of drivers(Firmwares) and interrupt handlers. Drivers are translate high level commands to hardware instructions. Interrupt handlers are used to transfer information between the main memory and the disk system.

## Virtual File System

Virtual File System allow os to support multiple File System in the same time. It provides an unified interface (VFS Interface) for users to do operations without knowing the implementations about operations of file systems. VFS has a file-representation structure, vnode containing a numerical designator for a network-wide unique file.

## File-System Implementation

File-system is installed in a disk partition. It has four major parts: **boot control block**, **volume control block**, **directory structure** and **per-file control block**.

**Boot control block** contains the information to boot the operating system and simply to say, it is the place to put OS itself.

**Volume control block** also called Superblock in Unix and Master File table in Windoes. It owns the volume details such as total number of blocks, free blocks, block size and free block pointers or array.

**Directory structure** 

**Per-file File Control Block(FCB)** contains details about the file. In NTFS, this information is sotred within the Master File table (A RDBS structure).

In-memory information is used for both file-system management and improvemnet of performance as caching. There are **in-memory mount table**, **in-memory directory structure**, **system-wide open-file table**, **per-process open-file table** and **buffers**.

**In-memory mount table** has the information about each mounted volume.

**In-memory directory structure** stores the information of recent accessed directories.

**System-wide open-file table** contains *copy of open file's FCB** and the FCB are shared among with other process. There are also other information storing here. 

**Per-process open-file table** has a pointer to the appropriate entry in the system-wide open-file table. Multiple per-process open-file tables can point to the same entry. There are other information storing in the table.

**Buffers** hold the file-system blocks when they are being read and write from disk.

## Directory Implementation
1. Linear List

2. Hash Table

## Allocation Methods

1. Contiguous Allocation

A file occupies a sequential blocks and result in high performance on file reading since the header of disk can read the whole file without moving head to far distance.

Files are easy to be put because disk only needs to know the numnber of blocks and the start position(block number).

However, it has a serious problem called **external fragmentation** which brokes the free space into piece of chunks that are hard to be used for data allocation. Thus, the compaction is needed to reduce the waste. Ex: Disk Defragmentation tool in Windows.

Another solution to solve the fragmentation is **extent**. If the amount of the continuous blocks are insufficient to put the whole file, another chunk of free continuous space is added through link. 

2. Linked Allocation

Linked Allocation is the best way to solve the external fregmentation. Data blocks are allowed to be separated over the disks and a link list can connect them all together. No compaction is needed. 

An issue comes up because every data block has to contain a pointer linking to its next data block that cause more waste of storage. The solution is to **clustering** multiple blocks into one **clustered block**. In this way, the storage for pointers is less. It also increases the search speed because the clustered data blocks are continuous that can reduce the seek time for header to find out the blocks. But like the continuos allocation, when a clustered block is partially used, the space **internal fregmentation** occurs. 

Another main issue of this implementation is the disk head cannot read multiple blocks in short time, instead, it has to move from one block to anther block that both are far from each other. Therefore, disks spend so many times on moving its head from here to there. 

To solve this, **FAT (File Allocation Table)** is introduced. The table stores all data blocks' number and pointers that links to their next data block then it is imported in the main memory which is faster on conducting sequential read. Although the performance for reading a whole file is the same, it provides a faster way when users want to access a specific data block.

Another reliability issue is that once there is a data block broken in the list, the data blocks linked after it are all invalid. Some systems use the double links but it increases the overheading of the storage.


3. Indexed Allocation

Indexed Allocation has a performance on random access. There are data blocks which store the indices



## Free-Space Management

1. Bit Vector

2. Linked List

3. Grouping (Modified Linked List)

4. Counting (Modified Linked List)

## Unified Buffer Cache

## Efficiency and Performance

Efficiency cares about how well the space is used while performance discuss about how fast the operations conduct.

# Chapter 12: Mass-Storage Structure

There two vital factors effect the performance of megnatic disks. First is **transfer rate** which is the trabsfer rate between drive and computer. The second one is **positioning time (random access time)** which is time to move disk arm to desired cylinder**(seek time)** and time to desired sector to rotate under the disk head **(rotational lantency)**.

Comparing to Megnatic Disk, a Solid-State Disk is much reliable and fast because there is no moving parts inside that means **no rotational lantency and seek time**. But it is much more expensive and has less capacity.

## Disk Structure

There are two major types:

1. Constant Linear Velocity (CLV)

The disk **increases its rotation speed** when its head move from outer circle to inner ones. Becides, to assure the transfer rate is fixed, the number of blocks in the outer circles is higher than in the inner circles.

Example: CD and DVD

2. Constant Angular Velocity (CAV)

Unlike the CLV that disks rotate differently when the head on different tracks, CAV's rotational speed is always the same. To assure the steady of data transfer rate when disks rotate, all the track have the same data sectors. Therefore, the inner tracks have higher density of data sectors.

Example: HD

## Disk Attachment

Host-Attached Storage: Devices talk to I/O buses through the I/O ports.

Network-Attached Storage (NAS): Storage devices that can be accessed through network.

Storage-Area Network (SAN): It's a storage network that users cannot access directly through internet, instead, users get the data through other services like http. It's common to be seen in IT business. 

## Disk Scheduling (Magnetic Disk)

The Time indices that are used to measure the Magnetic Disk Performance

1. Access Latency: (Average access time)

Access Latency = Average seek time (Time for the head to move from track to track) + Average rotational lantency (Rotate to the right position)

2. Average I/O time

Average I/O time = Average Access time + ( Amount to transfer / transfer rate ) + controller overhead

Here are several common Scheduling:



# Chapter 13: I/O Systems



# Chapter 14: System Protection

# Chapter 15: System Security

# Chapter 16: The Linux System

# Reference

* [Operating System Concepts 9th edition ](http://as.wiley.com/WileyCDA/WileyTitle/productCd-EHEP002013.html)
* [Wikipedia](https://www.wikipedia.org)

