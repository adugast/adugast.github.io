# Linux Overall

These information will cover ...

### Summary
1. Hardware
2. Boot-Sequence
3. Kernel
4. Linux System

## 1) Hardware
- Motherboard
- CPU
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
