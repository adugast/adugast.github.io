# The Not So Fast Linux Notions Guide   

![Type: Document](https://img.shields.io/badge/Type-Document-brightgreen.svg)   ![OS: Linux](https://img.shields.io/badge/OS-Linux-brightgreen.svg)   [![Website: ON](https://img.shields.io/badge/Website-ON-brightgreen.svg)](https://adugast.github.io/) : https://adugast.github.io/

-----------------------------------------------------------------------------------------

![Linux Logo](https://www.orkutel.com/images/icons/linux-logo_small.png)

## Summary

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
  I-time + E-time = Machine Cycle  
  (1) Fetch, (2) Decode, (3) Execute, (4) Store  
  Cache L1/ Cache L2 (Caches are memory in CPU: L1 very fast but very small, L2 more capacity than L1 but less fast. Placed on CPU chip)
- Random Access Memory (RAM)
  - Static Random Access Memory (SRAM)
  - Dynamic Random Acces Memory (DRAM): transistor and capasitor are paired to create a memory cell which represent a single bit of data
- Hard Disk, SSD

go further:
- Network board
  - Physical Network Interfaces: eth0, eth8, radio0, wlan19. Represents a NIC (Network Interface Controller)
  - Virtual Network Interfaces: lo, eth0:1, eth0.1, vlan2. Do not represent an existent hardware device but is linked to one.
  - NIC connects a computer to computer network. It's a component connected to the motherboard via PCI connectors, PCI-E, USB, Thunderbold, FireWire, ISA connector, ... and provide network via ethernet, wifi, fibre, fddi, token ring ...
  - Loopback interface, TUN/TAP interface, ...  
- Graphical Processing Unit (GPU)
- Von Neumann Architecture
- Electrical Components:   
  - Transistor: acts as a switch that lets the control circuitry on the memory chip to read the capacitor or change it state   
  - Capacitor   
- Difference NOR/NAND (MTD - Memory Technology Device)
  - NOR flash is byte-addressable. It's usually used in applications where a CPU needs to execute code from it directly, like BIOS or boot ROM firmware.   
  - NAND works in blocks somewhat like disks. So generally anything else, especially in memory card or storage device situations, is going to be NAND. Some NAND has a "Disk On Chip" mode where block 0 can be executed directly, but not any other blocks.  
- [MTD](http://www.linux-mtd.infradead.org/doc/general.html#L_overview)

## 2) Boot-Sequence

- Power-ON
- EEPROM
- Power-On Self-Test (POST)
  - Initializes the hardware: verify CPU registers, verify the integrity of the BIOS code itself
- MBR  
{  
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
- initrd
- initramfs: The only purpose of an initramfs is to mount the root filesystem: Then, it provides an adaptative way to load the rootfs from a network, load it from an LVM logical volume, having an encrypted rootfs where a password is required, or for the convenience of specifying the rootfs as a LABEL or UUID.  
It's an .gpio archive that contains files, tools, libraries, etc... During the boot, the bootloader give the initramfs to the kernel. The kernel creates a ramfs (or tmpfs if available) to be able to extract the content of the initramfs in the system. Then, it launches the init script located at the root of the tmpfs. The script mounts the rootfs, mounts and install all needed files and then, swap each others with the rootfs to finally call the /sbin/init to continue the boot process.


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

### Linux Kernel Structure

|       Components       |           Manage                                 |           Hardware                            |
|:----------------------:|:------------------------------------------------:|:----------------------------------------------|
| process management     | scheduler, signal handling, process/threads      | CPU                                           |
| memory management      | virtual memory and MMU                           | RAM                                           |
| filesystems            | filesystem types and block devices               | Hard Disk, floppy disk, CD                    |
| device drivers         | character devices                                | User peripherals (mouse, keyboard, audio, ..) |
| network management     | network drivers and network protocols            | Network Controller (ethernet or wifi)         |


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
- FUSE  
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

Processes: Page Table                                                                                                      
- Every process have it's own memory space                                                                                 
- Each address maps to a real address in physical memory                                                                   
- Processes have a page table in RAM that stares all their mapping (usually 4k blocks, normal size of a page)              
- every memory access uses the page table                                                                                  
- when you swith of process the kernel knwd wich page to use and the cpu uses it.                                          
- some pages don't map to a physical RAM address => CPU BAD ADDRESS "SEGMENTATION FAULT"

Memory Allocation algorythm:
  - Buddy memory allocation
  - Stack based memory allocation
  - Slab memory allocation

Linux MANUALS:   
```
use man man !    
```
Man pages are organized in 8 sections:

|       Section nbr       |           Manage                                                               |
|:-----------------------:|:-------------------------------------------------------------------------------|
| man 1                   | Executable programs or shell commands                                          | 
| man 2                   | System calls (functions provided by the kernel)                                | 
| man 3                   | Library calls (functions within program libraries)                             | 
| man 4                   | Special files (usually found in /dev)                                          | 
| man 5                   | File formats and conventions eg /etc/passwd                                    | 
| man 6                   | Games                                                                          | 
| man 7                   | Miscellaneous (including macro packages and conventions), e.g. man(7), groff(7)| 
| man 8                   | System administration commands (usually only for root)                         | 
| man 9                   | Kernel routines [Non standard]                                                 | 


## 5) IPC

- file                                                                                                              
- signal                                                                                                                                                                  
- sockets (network and uds)                                                                                         
- messages queue, mqueue                                                                                                    
- named pipes, mkfifo                                                                                                       
- pipes                                                                                                             
- shared memory

## 6) Socket Programming

- TCP - Transmission Control Protocol                                                                                                          
- UDP - User Datagram Protocol                                                                                                               
- RAW                                                                                                               
- UDS - Unix Domain Socket                                                                                                               
- netlink - communication between kernel and user space

## 7) OSI Model - Open System Interconnection

| Level | Layer Name      |           Manage                                          |           Hardware                            |
|------:|:---------------:|:---------------------------------------------------------:|:----------------------------------------------|
| 7     | application     | web browser, http, ftp, dns, telnet, smtp, ssh, snmp, nfs | Allow access to network resource
| 6     | presentation    | SSL, TLS, ASCII, jpeg, gif, html                          | Translate, encrypt, compress data
| 5     | session         | Socket RPC                                                | Establish, manage and terminate sessions
| 4     | transport       | TCP UDP SPX                                               | Provide reliable message delivery and error recovery
| 3     | network         | IP IPX Appletalk                                          | Move packets from source to destination and provide networking |
| 2     | data            | ethernet, token ring, 802.11                              | Organize bits into frames and provide hop-to-hop delivery   |
| 1     | physical        | copper, fiber, antenna (electric, light, radio signals)   | Transmit bits over a medium and provide mechanical and electrical specifications |

data encapsulation principles

go further:                                                                                                             
- tcp 3-way handshake
```
     Host1            Host2                                                                                            
1-    syn     ----->                                                                                                    
2-            <-----  syn/ack                                                                                           
3-   ack/data ----->

Host A sends a TCP SYNchronize packet to Host B                                                                         
Host B receives A's SYN                                                                                                 
Host B sends a SYNchronize-ACKnowledgement                                                                              
Host A receives B's SYN-ACK                                                                                             
Host A sends ACKnowledge                                                                                                
Host B receives ACK.                                                                                                    
TCP socket connection is ESTABLISHED.  
```
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

Network architecture:
  - Peer-to-Peer (P2P)
  - Client-Server

## 10) Unit Test

Test Doubles:
- faking
- mocking
- stubbing

[Difference between fakes, mocks and stubs](https://blog.pragmatists.com/test-doubles-fakes-mocks-and-stubs-1a7491dfa3da)

## 11) Machine Learning, AI, and Neuronal Network

## 12) Quantum Computing

[Quantum Computers Explained](https://www.youtube.com/watch?v=JhHMJCUmq28)

## 13) Best References

- [The Linux Documentation Project](https://www.tldp.org/LDP/tlk/)
- [How The Internet Works](https://www.youtube.com/playlist?list=PLzdnOPI1iJNfMRZm5DDxco3UdsFegvuB7)
- [Beej's Guide to Network Programming](http://beej.us/guide/bgnet/html/single/bgnet.html)
- [Linux Input Subsystem](https://www.kernel.org/doc/html/v4.15/input/input_uapi.html)
- [OSDev](https://wiki.osdev.org/Main_Page)
- [Shichao's Notes](https://notes.shichao.io/apue/)

## Powered by

- [GitHub Pages](https://pages.github.com/)
- [Stackedit - In-browser Markdown editor](https://stackedit.io/app#)
- [GitHub - adugast](https://github.com/adugast)
