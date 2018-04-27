# Linux Overall

This course will cover ...

### Summary
1. Hardware
2. Boot-Sequence
3. Kernel
4. Linux System
5. IPC
6. Socket Programming
7. OSI Model
8. Embedded Linux
9. What is the internet (Code.org)

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

## 3) Kernel
- process management - scheduler, signal handling, process/threads      OVER CPU                                        
- memory management - virtual memory and MMU                            OVER RAM                                        
- filesystems management - filesystem type describe by a block device   OVER Hard Disk, floppy disk, CD                 
- device drivers - character device                                     OVER Peripherals (mouse, keyboard, audio, ..)   
- network management - network drivers and network protocols            OVER Network Controller (ethernet or wifi)

## 4) Linux System

POSIX: Portable Operating System Interface (standard, norme)                                                               
                                                                                                                           
C lib
- common header files: stdlib, unistd, stdio, string                                                               
- variable and limit: stdbool, stdint, limits                                                                      
- socket headers                                                                                                   
- API header: syslog, inotify, regex, ncurses, pthread...                                                          
                                                                                                                           
elf format and object code                                                                                                 
compiler                                                                                                                   
GCC:                                                                                                                       
    * compilation from .c to .o                                                                                            
    * linkage of symbols in one bin                                                                                        
                                                                                                                           
Filesystems: rootfs, procfs, sysfs, autofs, nfs                                                                            
FSH:                                                                                                                       
                                                                                                                           
Daemons                                                                                                                    
    * ntpd                                                                                                                 
    * syslogd                                                                                                              
    * watchdogd                                                                                                            
    * sshd                                                                                                                                                                    
    * inetd/xinetd (extended internet daemon)

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

platform requirement -> arm, mips, xtensa, intel, amd, powerpc                                                          
buildroot -> generates toolchain to compile corresponding bootloader, kernel, rootfs                                    
qemu -> lightweight virtualization

## 9) Internet

1) [What is the internet ?](https://www.youtube.com/watch?v=Dxcc6ycZ73M)
2) [The internet: Wires, Cables, Wifi](https://www.youtube.com/watch?v=ZhEf7e4kopM)
3) [The Internet: IP Addresses & DNS](https://www.youtube.com/watch?v=5o8CwafCxnU)
4) [The Internet: Packets, Routing & Reliability](https://www.youtube.com/watch?v=AYdF7b3nMto)
5) [The Internet: HTTP & HTML](https://www.youtube.com/watch?v=kBXQZMmiA4s)
6) [The Internet: Encryption & Public Keys](https://www.youtube.com/watch?v=ZghMPWGXexs)
7) [The Internet: Cybersecurity & Crime](https://www.youtube.com/watch?v=AuYNXgO_f3Y)
8) [The Internet: How Search Works](https://www.youtube.com/watch?v=LVV_93mBfSU)
