### ELF

~~~

     ┌────────────────┐
     │                │
     │  ELF header    │
     │                │
     │                │
     └────────────────┘

     ┌────────────────┐
     │                │
     │  Program Header│
     │                │
     │                │
     └────────────────┘

     ┌────────────────┐
     │                |
     │  .text         |
     │                │
     │                │
     │                │
     └────────────────┘


     ┌────────────────┐
     │                │
     │   .rodata      │
     │                │
     │                │
     └────────────────┘

     ┌────────────────┐
     │                │
     │    .data       │
     │                │
     │                │
     └────────────────┘
      
      ...
      
     ┌────────────────┐
     │                |
     │  section header|
     │                │
     │                │
     │                │
     └────────────────┘

~~~

`readelf -a` and `hexdump -C` will print the ELF contents.
Use `objdump -s -d .o` to get the asm code of the ELF, this is same as .text from above.
Use `objdump -h .elf` to get sections.

The ELF header `readelf -h` is 32 bytes long, and identifies the format of the file. It starts with a sequence of four unique bytes that are 0x7F followed by 0x45, 0x4c, and 0x46 which 
translates into the three letters E, L, and F. Among other values, the header also indicates whether it is an ELF file for 32 or 64-bit format, uses little or big endianness,
shows the ELF version as well as for which operating system the file was compiled for in order to interoperate with the right application binary interface (ABI) and cpu 
instruction set.

The program header `readelf -l` shows the segments used at run-time, and tells the system how to create a process image. The header from Listing 2 shows that the ELF file consists of 9 
programheaders that have a size of 56 bytes each, and the first header starts at byte 64.

The third part of the ELF structure is the section header `read -S`. It is meant to list the single sections of the binary. The switch -S (short for –section-headers or –sections) lists
the different headers. As for the touch command, there are 27 section headers, and Listing 5 shows the first four of them plus the last one, only. Each line covers the section
size, the section type as well as its address and memory offset.






### APK

### EXE

<a href="#top">Back to top</a>
