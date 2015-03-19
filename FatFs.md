# From the FatFs home page #

FatFs is a generic file system module to implement the FAT file system to small embedded systems. The FatFs is written in compliance with ANSI C, therefore it is independent of hardware architecture. It can be incorporated into cheap microcontrollers, such as 8051, PIC, AVR, SH, Z80, H8, ARM and etc..., without any change.

The FatFs home page is http://elm-chan.org/fsw/ff/00index_e.html.

# Features of FatFs #

  1. Separated buffer for FAT structure and each file, suitable for fast multiple file access.
  1. Supports multiple drives and partitions.
  1. Supports FAT12, FAT16 and FAT32.
  1. Supports 8.3 format file name. (LFN is not supported)
  1. Supports two partitioning rules: FDISK and Super-floppy.
  1. Optimized for 8/16-bit microcontrollers.

# Features of Petit FatFs (different from FatFs) #

  1. Very low memory consumption, suitable for small memory system. (1KB RAM)
  1. Supports only single drive.