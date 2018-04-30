# The Not So Fast Linux Notions Guide

![Linux Logo](https://www.orkutel.com/images/icons/linux-logo_small.png)

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
10. Unit Test
11. Machine Learning, AI and Neuronal Network
12. Quantum Computing
13. Best Resources

## 1) Hardware

- Motherboard -> link every computer components and host the EEPROM.
- Central Processing Unit (CPU)
  - Control Unit (CU)
  - Arithmetic/Logic Unit (ALU)
  I-time + E-time = Machine Cycle</br>
  (1) Fetch, (2) Decode, (3) Execute, (4) Store
  Cache L1/ Cache L2
- Random Access Memory (RAM)
  - Static Random Access Memory (SRAM)
  - Dynamic Random Acces Memory (DRAM): transistor and capasitor are paired to create a memory cell which represent a single bit of data
- Hard Disk

go further:
- Network board
- Graphical Processing Unit (GPU)
- Von Neumann Architecture
- Transistor: acts as a switch that lets the control circuitry on the memory chip to read the capacitor or change it state
- Capacitor

## 2) Boot-Sequence

- Power-ON
- EEPROM
- Power-On Self-Test (POST)
  - Initializes the hardware: verify CPU registers, verify the integrity of the BIOS code itself
- MBR</br>
{</br>
&nbsp;&nbsp;&nbsp;&nbsp;bootstrap code - call the kernel (446 bytes)                                                                     
&nbsp;&nbsp;&nbsp;&nbsp;partition table (4 * 16 bytes = 64 bytes)                                                                        
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;partition1                                                                                                   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;partition2                                                                                                   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;partition3                                                                                                   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;partition4                                                                                                   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;bootsignature (2 bytes, magic number 0x55AA)                                                                 
}                                                                                                                      
so 446 + 4*16 + 2 = 512 bytes
- Kernel
- Init System

go further:
- difference BIOS/MBR, UEFI/GUID
- initrd, initramfs            

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

go further:
- CFS and red-black tree algorithm                                                                                      
- page table with MMU                                                                                                   
- TLB - Translation Lookaside Buffer                                                                                    
- process and memory management stack and heap (+sections)                                                              
  - sections: bss, data, text                                                                                           
  - assembly, cpu registers                                                                                             
- difference between block and character device (stream and page)                                                       
- network drivers and protocols at kernel level                                                                         

## 4) Linux System

POSIX: Portable Operating System Interface (standard, norme)                                                               
                                                                                                                           
C lib

- common header files: stdlib, unistd, stdio, string                                                               
- variable and limit: stdbool, stdint, limits                                                                      
- socket headers                                                                                                   
- API header: syslog, inotify, regex, ncurses, pthread...                                                          
                                                                                                                           
Elf format and object code:


GCC:                                                                                                                    
- compilation from .c to .o                                                                                            
- linkage of symbols in one binary                                                                                        
                                                                                                                           
Filesystems:
- rootfs
- procfs
- sysfs
- autofs
- nfs 
- ...

FHS - Filesystem Hierarchy Standard
[Linux Filesystem Hierarchy](http://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/Linux-Filesystem-Hierarchy.html)

System Daemons:                                                                                                                  
- ntpd                                                                                                                 
- syslogd                                                                                                              
- watchdogd                                                                                                            
- sshd                                                                                                                                                                    
- inetd/xinetd (extended internet daemon)

Mutexes:                                                                                                                
- semaphores                                                                                                            
- futex                                                                                                                 
- compare and swap                                                                                                      
- atomic instruction

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

go further:                                                                                                             
- tcp handshake                                                                                                         
- router, switch, dns, hub, ...

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

go further:
- SFPs, ASIC/FPGA, CPLD, PCB, PCI, IC, I2C, SCSI
- bus                                                                                                                   
- ARP: Address Resolution Protocol. ARP table in routers to map IP address to mac address                               
- Udev: Device manager for linux kernel                                                                                                                                                                          
- Makefile, Cmake                                                                                                       
- Agile Methodology: Scrum, DevOps                                                                                      
- Network hardware: ROUTER, BRIDGE, SWITCH, NAT network adress translation                                              
- DNS: /etc/resolv.conf

## 9) Internet

![Code.org Logo](https://upload.wikimedia.org/wikipedia/commons/f/f4/Code.org_logo.svg)

1. [What is the internet ?](https://www.youtube.com/watch?v=Dxcc6ycZ73M)
2. [The internet: Wires, Cables, Wifi](https://www.youtube.com/watch?v=ZhEf7e4kopM)
3. [The Internet: IP Addresses & DNS](https://www.youtube.com/watch?v=5o8CwafCxnU)
4. [The Internet: Packets, Routing & Reliability](https://www.youtube.com/watch?v=AYdF7b3nMto)
5. [The Internet: HTTP & HTML](https://www.youtube.com/watch?v=kBXQZMmiA4s)
6. [The Internet: Encryption & Public Keys](https://www.youtube.com/watch?v=ZghMPWGXexs)
7. [The Internet: Cybersecurity & Crime](https://www.youtube.com/watch?v=AuYNXgO_f3Y)
8. [The Internet: How Search Works](https://www.youtube.com/watch?v=LVV_93mBfSU)

## 10) Unit Test

Test Doubles:
- faking
- mocking
- stubbing

[Difference between fakes, mocks and stubs](https://blog.pragmatists.com/test-doubles-fakes-mocks-and-stubs-1a7491dfa3da)

## 11) Machine Learning, AI, and Neuronal Network

## 12) Quantum Computing

[Quantum Computers Explained](https://www.youtube.com/watch?v=JhHMJCUmq28)

## 13) Best Resources

- [The Linux Documentation Project](https://www.tldp.org/LDP/tlk/)
- [How The Internet Works](https://www.youtube.com/playlist?list=PLzdnOPI1iJNfMRZm5DDxco3UdsFegvuB7)
- [Beej's Guide to Network Programming](http://beej.us/guide/bgnet/html/single/bgnet.html)
- [Linux Input Subsystem](https://www.kernel.org/doc/html/v4.15/input/input_uapi.html)

## Powered by

- [GitHub Pages](https://pages.github.com/)
- [Stackedit - In-browser Markdown editor](https://stackedit.io/app#)
- [GitHub - pestbuns](https://github.com/pestbuns)
