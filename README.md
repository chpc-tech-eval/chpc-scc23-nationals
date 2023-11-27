CHPC 2023 Student Cluster Competition
========================================
Benchmarking and Competition instructions for the Center for High Performance Computing (CHPC) 2023 Student Cluster Compettion (SCC). Which is hosted by the National Integrated Cyber Infrastructure Systems (NICIS), a division of the South African Council for Scientific and Industrial Research (CSIR). For 2023 the competition will be held in person at the Kruger Gate Hotel in Mpumalanga, South Africa.

# Getting Started
------------------

The benchmarks were chosen to be compatible with the software environment that you previously setup in the first round of this competition. For this round, you are allowed to install any legally obtained software you wish to run the problems. However, using obscure, nonstandard software may limit the support you receive from the competition organizers. 

You are strongly encouraged to make use of any resource available to you. However, be advised that the competition organizers will provide limited technical support and assistance in building and running your applications. 

Team mentors are encouraged to support and motivate their teams. However, they may not do any of the work for the students. They are strictly there to provide guidance and suggestions, and are there to participate in the conference for their own benefit as well. 

Team captains will each be issued a competition USB flash drive. This is how the teams will be issued with their benchmarks and how teams will submit their results. Only the Team captain can approach the organizers’ booth, to submit and/or receive benchmarks. Only one Team captain is allowed at the organizer's booth at any time. 

To receive the next set of benchmarks, you will need to make a valid submission of the previous benchmark. Alternatively, you may forfeit penalty points should you be unable to submit a preceding result but want to attempt the next benchmark. The benchmarks will get progressively harder. 

The competition organizers will give teams a general indication of where they should be, in the morning at the beginning of the day, and again in the afternoon at the end of the day.

The competition will end on **Thursday, 7<sup>th</sup> of December at 10:00am**.

Rulings and decisions from the competition organizers are final. 

Good Luck! 

# Timetable
-------------

# Scoring
----------

| Application          | Weight | Breakdown                                                                                               |
| ---                  |    --- | ---                                                                                                     |
| HPCC & HPCG          |    20% | <ul><li>HPCC *[7.5%]*<ul><li>High Performance Linpack (HPL) *[5%]*</li></ul><li>HPCG *[7.5%]*</li></ul> |
| OpenFOAM             |    10% |                                                                                                         |
| AmberMD              |    10% |                                                                                                         |
| WRF                  |    10% |                                                                                                         |
| SwiftSIM             |    10% |                                                                                                         |
| MILC                 |    10% |                                                                                                         |
| *Secret Application* |    10% |                                                                                                         |
| Presentation         |    20% |                                                                                                         |

# Instructions for Mentors
---------------------------

# Cheat Sheet
-------------- 

Below is a table with a number of Linux system commands and utilities that you *may* find useful in assisting you to debug problems that you may encounter with your clusters. Note that some of these utilities do not ship with the base deployment of a number of Linux flavors, and you may be required to install the associated packages, prior to making use of them.

| Command            | Description                                                                                                                                                                                                        |
| ---                | ---                                                                                                                                                                                                                |
| ssh                | Used from logging into the remote machine and for executing commands on the remote machine.                                                                                                                        |
| scp                | SCP copies files between hosts on a network. It uses ssh for data transfer, and uses the same authentication and provides the same security as ssh.                                                                |
| wget / curl        | Utility for non-interactive download of files from the Web.It supports HTTP, HTTPS, and FTP protocols.                                                                                                             |
| top / htop / btop  | Provides a dynamic real-time view of a running system. It can display system summary information as well as a list of processes or threads.                                                                        |
| screen / tmux      | Full-screen window manager that multiplexes a physical terminal between several processes (typically interactive shells).                                                                                          |
| ip a               | Display IP Addresses and property information                                                                                                                                                                      |
| dmesg              | Prints the message buffer of the kernel. The output of this command typically contains the messages produced by the device drivers                                                                                 |
| watch              | Execute a program periodically, showing output fullscreen.                                                                                                                                                         |
| df -h              | Report file system disk space usage.                                                                                                                                                                               |
| ping               | PING command is used to verify that a device can communicate with another on a network.                                                                                                                            |
| lynx               | Command-line based web browser (more useful than you think)                                                                                                                                                        |
| ctrl+alt+[F1...F6] | Open another shell session (multiple ‘desktops’)                                                                                                                                                                   |
| ctrl+z             | Move command to background (useful with ‘bg’)                                                                                                                                                                      |
| du -h              | Summarize disk usage of each FILE, recursively for directories.                                                                                                                                                    |
| lscpu              | Command line utility that provides system CPU related information.                                                                                                                                                 |
| lstotp             | View the topology of a Linux system.                                                                                                                                                                               |
| inxi               | Lists information related to your systems' sensors, partitions, drives, networking, audio, graphics, CPU, system, etc...                                                                                           |
| hwinfo             | Hardware probing utility that provides detailed info about various components.                                                                                                                                     |
| lshw               | Hardware probing utility that provides detailed info about various components.                                                                                                                                     |
| proc               | Information and control center of the kernel, providing a communications channel between kernel space and user space. Many of the preceding commands query information provided by proc, i.e. `cat /proc/cpuinfo`. |
| uname              | Useful for determining information about your current flavor and distribution of your operating system and its version.                                                                                            |
| lsblk              | Provides information about block devices (disks, hard drives, flash drives, etc) connected to your system and their partitioning schemes.                                                                          |
|                    |                                                                                                                                                                                                                    |





