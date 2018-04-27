# Linux Overall

### Summary

1. Hardware
2. Boot-Sequence
3. Kernel
4. Linux System
5. IPC
6. Socket Programming
7. OSI Model
8. Embedded Linux
9. Internet (Code.org)
10. Unit Test (UT)
11. Machine Learning, AI and Neuronal Network

## 1) Hardware

- Motherboard
- Central Process Unit (CPU)
Composed of:
  - Control Unit (CU)
  - Arithmetic/Logic Unit (ALU)
I-time + E-time = Machine Cycle -> (1) Fetch, (2) Decode, (3) Execute, (4) Store
- RAM
- Hard Disk

## 2) Boot-Sequence

- Power ON
- EEPROM
- Power-On Self-Test (POST)
- MBR
- Kernel
- Init System

different initsystems:                                                                                                 
- s6                                                                                                                
- systemd(debian)                                                                                                   
- upstart(ubuntu)                                                                                                   
- openRC                                                                                                            
- initng                                                                                                            
                                                                                                                        
different bootloaders:                                                                                                 
- GNU GRUB (GRand Unified Bootloader)                                                                               
- LILO (Linux Loader)                                                                                               
- BURG (New bootloader)                                                                                             
- Syslinux

## 3) Kernel

- process management - scheduler, signal handling, process/threads      OVER CPU                                        
- memory management - virtual memory and MMU                            OVER RAM                                        
- filesystems management - filesystem type describe by a block device   OVER Hard Disk, floppy disk, CD                 
- device drivers - character device                                     OVER Peripherals (mouse, keyboard, audio, ..)   
- network management - network drivers and network protocols            OVER Network Controller (ethernet or wifi)

Types:                                                                                                                  
- Microkernel (as Hurd): small kernel space, big user space (due to the lack of drivers support, drivers not part of kernel -> in user space)
- Monolithic (as Linux)                                                                                             
- Hybrid (boundaries between micro and monolithic kernels)                                                          
                                                                                                                        
Modularity:                                                                                                        
- Loadable Kernel Module (LKM)

## 4) Linux System

POSIX: Portable Operating System Interface (standard, norme)                                                               
                                                                                                                           
C lib

- common header files: stdlib, unistd, stdio, string                                                               
- variable and limit: stdbool, stdint, limits                                                                      
- socket headers                                                                                                   
- API header: syslog, inotify, regex, ncurses, pthread...                                                          
                                                                                                                           
Elf format and object code                                                                                                 
                                                                                                                 
GCC                                                                                                                    

- compilation from .c to .o                                                                                            
- linkage of symbols in one binary                                                                                        
                                                                                                                           
Filesystems

- rootfs
- procfs
- sysfs
- autofs
- nfs 
- ...

File System Hyerarchy (FHS)                                                                                                                       
                                                                                                                           
System Daemons                                                                                                                    

- ntpd                                                                                                                 
- syslogd                                                                                                              
- watchdogd                                                                                                            
- sshd                                                                                                                                                                    
- inetd/xinetd (extended internet daemon)

## 5) IPC

- file                                                                                                              
- signal                                                                                                                                                                  
- sockets (network and uds)                                                                                         
- messages queue                                                                                                    
- named pipes                                                                                                       
- pipes                                                                                                             
- shared memory

## 6) Socket Programming

- TCP                                                                                                               
- UDP                                                                                                               
- RAW                                                                                                               
- UDS                                                                                                               
- netlink - communication between kernel and user space

## 7) OSI Model - Open System Interconnection

7- application - web browser, http, ftp, dns, telnet, smtp, ssh, snmp, nfs                                              
6- presentation - SSL, TLS, ASCII, jpeg, gif, html                                                                      
5- session - Socket RPC                                                                                                 
4- transport - TCP UDP SPX                                                                                              
3- network - IP IPX Appletalk                                                                                           
2- data - ethernet, token ring, 802.11                                                                                  
1- physical - copper, fiber, antenna (electric, ligth, radio signals)

data encapsulation principles

## 8) Embedded Linux

Platform requirement -> arm, mips, xtensa, intel, amd, powerpc      

Buildroot

Buildroot is a build embedded system automation.
It provides a simple, efficient and easy-to-use tool to generate embedded Linux systems through cross-compilation.

Generates:
- Toolchain: Cross compilation (provides linked, compiler and build utilities i.e make)
- Bootloader: Loads kernel in memory
- Kernel: Abstraction on hardware layer
- Rootfs: Userspace

Similar project:
- LTIP
- Yocto
- OpenWRT
- OpenEmbedded
- PTXdist

Qemu

Qemu is a generic, lightweight and open source machine emulator and virtualizer

Busybox

The Swiss Army Knife of Embedded Linux

## 9) Internet

![enter image description here](https://upload.wikimedia.org/wikipedia/commons/f/f4/Code.org_logo.svg)

1. [What is the internet ?](https://www.youtube.com/watch?v=Dxcc6ycZ73M)
2. [The internet: Wires, Cables, Wifi](https://www.youtube.com/watch?v=ZhEf7e4kopM)
3. [The Internet: IP Addresses & DNS](https://www.youtube.com/watch?v=5o8CwafCxnU)
4. [The Internet: Packets, Routing & Reliability](https://www.youtube.com/watch?v=AYdF7b3nMto)
5. [The Internet: HTTP & HTML](https://www.youtube.com/watch?v=kBXQZMmiA4s)
6. [The Internet: Encryption & Public Keys](https://www.youtube.com/watch?v=ZghMPWGXexs)
7. [The Internet: Cybersecurity & Crime](https://www.youtube.com/watch?v=AuYNXgO_f3Y)
8. [The Internet: How Search Works](https://www.youtube.com/watch?v=LVV_93mBfSU)

## 10) Unit Test (UT)

Test Doubles:
- faking
- mocking
- stubbing

[Difference between fakes, mocks and stubs](https://blog.pragmatists.com/test-doubles-fakes-mocks-and-stubs-1a7491dfa3da)

## 11) Machine Learning, AI, and Neuronal Network
