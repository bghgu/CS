# UNIX

## 1. Computer Systems

* Computer Systems : Hardware + Software, Without its Software, a computer is useless.
* Hardware : Central PRocessing Unit(CPU), Memory, Disks, Monitor, Keyboard
* With its Software, a Compute can store, process, and retrieve information, and engage in many other valuable activites.

## 2. Computer Software

* System Programs that manage the operation of the computer itself
* Application Programs, which solve problems for their users.

## 3. Operationg System

- most fundamental of all the system program
- controls all the computer`s resources
- provides the base for the application programs
  - DOS, Windows, Linux, MacOS, Android, etc....

* Unix is a popular Operating System.
  * It is most commonly used in backend applications, on servers, powerful workstations, etc
  * One of the most well-designed operationg system of its time.
  * UNIX is available for virtually all platforms
* Linux and MacOS X (basically a BSD Unix) are popluar desktop alternatives to MS Windows.
* a Program that controls the execution of application programs and acts as an interface between the user of a computer an the computer hardware.
* An Operating System has four Major Components:
  * process management
  * input / output
  * memory management
  * file system
  * communication

## 4. Unix

* Common Operating System
* Open Platform
* Runs on Many Machines
* Widely Used
* Features
  * Time Sharing
  * Multiuser
  * Networking
  * Interactive

## 5. Unix Utilities

* Standard UNIX comes complete with at least 200 small utility programs
  * shells
  * editors
  * C compiler
  * matching with regular expressions
  * searching
  * a sorting utility
  * software development tools
  * text-processing tools
* Graphical User Interfaecs
  * based on X Windows.
  * The most popular: CDE, Gnome, KDE
* Popular packages like spreadsheets, compilers, and desktop-publishing tools are also commercially available
* Unix is  an Open System, which means that the internal software architecture is well documented and available in source-code form for a relatively small fee
* Features of UNIX such as parallel processing, inter-process communication, and file handling are all easily accessible from a programming language such as C via a set of library routines knows as system calls

## 6. Summary of Unix Features

* 

## 7. Unix Philosophy

* Small is beautiful
  * Easy to Understand
  * Easy to maintain
  * More efficient
  * Better for reuse
* Make each program do one thing well
  * More complex functionality by combining programs
  * Make every program a filter
  * These small utilities should be combined to accomplish more complex tasks.
* Portability over efficiency
  * Most efficient implementation is rarely portable
  * Portability better for rapidly changing hardware
* Use flat ASCII files
  * Common, simple file format(XML)
  * Example of portability over efficiency
* Reusable code
  * Good Programmeres write good code, greate programmers borrow good code
* Silence is golden
  * Only report if something is wrong
* Think hierarchically

## 8. Unix Yesterday

* A computer scientist named Ken Thompson at Bell Laboratories Built the first version of UNIX
  * Called UNICS
  * written by using assembly language
  * only a single-user system
  * no network capability
  * poor memory-management system for sharing memory between processes
* A few years later, a colleague of Ken`s Dennis Ritchie, Suggested that they rewrite UNIX using the C Language.
  * the UNIX System suddenly had a huge advantage over other operationg systems - its source code was understandable
  * Only a small percentage of the original source code remained in assembly language, which meant the porting the operationg system to a diffenent machine was quiete easy
  * Unix was not commercialized originally
* The University of California at Berkeley, made some huge omporvements over the years, including the first good memory-management system and the first real networking capability.
* UC Berkeley offered a version of  UNIX, called BSD(Berkeley Standard Distribution) to the general public.
* Variations
  * UNIXWARE
  * Solaris
  * SCO UNIX
  * IRIX
  * HP-UX
  * DEC-OSF/1
  * AIX
  * LINUX
  * A/UX
* UNIX System V Release 4
  * Unified command set
  * Shells, User Interfaces
  * Directory Tree
  * I/O and System Access
  * Real-Time Processing
  * System Administration
  * Networking
  * Internationalization
  * Application Development
  * File Systems and Operations
  * Memory Management

## 9. Unix Today

* A more recent entry into the UNIX world is Linux, a free version of UNIX written by a student in Finland and now marketed and supported by several different compaines.

## 10. Why UNIX Important

* Open Source Code
* Cooperative Tools and Utilities
* Multi-User / Multi-Tasking
* Excellent Networking
* Portability
* Applications
* Utilities
* File System
* Shell
* Kernel : the system core

## 11. Shell

* It is the command line interface
* The Three most common
  * Bourne : The basic shell
  * Korn : An improved Bourne
  * C : Syntax similar to C

## 12. Why is Unix popular?

* OS can handle advanced hardware - Easy to scale up
* Open System - not proprietary
* Written in HLL - C
* Source code is available
* Designed to be multiuser
* Cross Platform standard

## 13. Linux

* Free Software Foundation
* GNU - Gnu`s Not Unix
* Richard Stallman
  * Created
    * Copyleft
    * GPL
    * EMACS

## 14. How can UNIX run on so many machines?

* Developed in C
* Only a small part in Assembly

## 15. Overview of Unix System & More Features

### Overview of Unix System

* Utilities
* Multiuser
* Multitasking
* System Kernel
* File Structure
* Security
* Shells
* Filename Pattern matching
* Device Independent I/O
* Interprocess Communications

### More Features

* Job Control
* Electronic Mail
* Screen ORiented Editor - vi
* scrolling thru a file
* Networking Utilites
* Shell functions
* Graphical User Interfaces
* System Administration

## 16. The Unix System

* Multiuser
  * Server - connect via terminals
* Single User
  * Your own PC
* Interface
  * Text based
  * GUI

## 17. What the difference between PC & Workstation

* Previously
  * Memory, Hard Drive, Screen
* Currently - OS is designed for
  * Windows, Mac OS = PC
  * Unix = Workstation

## 18. Basics

* Unix is  Case Sensitive
  * CD FILE != cd file
* Type mostly in lowercase
* Backspace
  * Either Backspace or Delete key or Ctrl + H
* Logging in
  * Username(Login ID) : a unique name that distinguishes you from the other users of the system.
  * Usernames and initail passwords are assigned to you by the system administrator(root-super user)
* User Accounts
  * Typically : first inital lastname
    * John Doe = jdoe
    * Im Hyunmi = jim
    * Daseul Bae = dbae
  * password
    * passwd
    * passwords must be 6+ characters Must be a good mix letters / digits
* Logging Off
  * exit
  * logout
  * Ctrl + D (^D)
  * Depends on yout version of Unix
* Turning Off a Unix System (If you are the owner / root)
  * Ctrl - ALT - DEL
  * init 5
  * shutdown now
  * halt
  * Depends on your version of UNIX

## 19. Shells

* See either a $, a % or another prompt
  * default shell prompting - a special kind of program
* A Shell
  * a middleman between you and the raw UNIX operationg system.
  * run programs, build pipelines of processes, save output to files, and run more that one program at the same time.
  * executes all of the commands
* most popular shells
  * Bourne Shell (sh)
  * Korn Shell (ksh)
  * C Shell (csh)
  * Bash Shell (bash)

## 20. Utility

* ls : Display list of file
* cat : Display content of file
* more : Display file w /pause
* cp : Copy file
* grep : Find string in file
* diff : Compare files
* mv : Rename file
* man : Get help
* chmod : Change file protection
* cd : Create directory
* mkdir : Make directory
* rmdir : Remove directory
* df : Display disk space
* vi : Edit a file
* lp : print a file
* date : Display Date / Time
* who, w : Who else is online
* cal : Display a calender
* finger : Displays info about a user
* talk : Chat with other user
* head : First few lines of the file
* tail : Last few lines of a file
* echo : Displays text
* man : Online manuals
* compress : Compress a file
* uncompress : Uncompress a file
* file : Displays information
* zcat : Display a compressed file

## 21. File Structure

* Files : Everything is a file
* Filenames
  * Characters
    * A-Z, a-z, Case Sensitive
    * 0-9 Digits
    * _ Underscore
    * . Period
  * Length: 255 Characters
* Invisible Filename
  * Start with a period
    * .hidden
    * .login
    * .profile
  * ls -a displays all filenames
* File Extensions
  * .c : C Program
  * .cc : C++ Programs
  * .csh : C shell script
  * .h : Header
  * .o : Object file
  * .sh : Sjell program
  * .tar : Archived using TAR
  * .uu : UUencoded File
  * .Z : compress file
* Directories
  * Adds a level of organization
  * Tree based
  * Starts at / (root)
* Special Directories
  * / : root
  * /dev : I/O devices - disks
  * /etc : sys admin stuff
  * /opt : applications
  * /home : user directories
  * /tmp : temporary files
  * /var : system variables
  * /bin : commands
  * /usr : commands, libraries