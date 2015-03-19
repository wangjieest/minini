# Adapting minIni to a file system #

The minIni library must be configured for a platform with the help of a so- called "glue file". This glue file contains macros (and possibly functions) that map file reading and writing functions used by the minIni library to those provided by the operating system. The glue file must be called "minGlue.h".

To get you started, the minIni distribution comes with the following example glue files:

  * a glue file that maps to the standard C/C++ library (specifically the file I/O functions from the "stdio" package),
  * a glue file for Microchip's "Memory Disk Drive File System Library" (see http://www.microchip.com/),
  * a glue file for the FAT library provided with the CCS PIC compiler (see http://www.ccsinfo.com/)
  * a glue file for the EFS Library (EFSL, http://www.efsl.be/),
  * and a glue file for the FatFs and Petit-FatFs libraries (http://elm-chan.org/fsw/ff/00index_e.html).

The minIni library does not rely on the availability of a standard C library, because embedded operating systems may have limited support for file I/O. Even on full operating systems, separating the file I/O from the INI format parsing carries advantages, because it allows you to cache the INI file and thereby enhance performance.

The glue file must specify the type that identifies a file, whether it is a handle or a pointer. For the standard C/C++ file I/O library, this would be:

```
#define INI_FILETYPE        FILE*
```

If you are _not_ using the standard C/C++ file I/O library, chances are that you need a different handle or "structure" to identify the storage than the ubiquitous "`FILE*`" type. For example, the glue file for the FatFs library uses the following declaration:

```
#define INI_FILETYPE        FIL
```

The minIni functions declare variables of this `INI_FILETYPE` type and pass these variables to sub-functions (including the glue interface functions) by reference.

For "write support", another type that must be defined is for variables that hold the "current position" in a file. For the standard C/C++ I/O library, this is "`fpos_t`".

Another item that needs to be configured is the buffer size. The functions in the minIni library allocate this buffer on the stack, so the buffer size is directly related to the stack usage. In addition, the buffer size determines the maximum line length that is supported in the INI file and the maximum path name length for the temporary file. For example, `minGlue.h` could contain the definition:

```
#define INI_BUFFERSIZE      512
```

The above macro limits the line length of the INI files supported by minIni to 512 characters.

The temporary file is only used when writing to INI files. The minIni routines copy/change the INI file to a temporary file and then rename that temporary file to the original file. This approach uses the least amount of memory. The path name of the temporary file is the same as the input file, but with the last character set to a tilde ("~").

Below is an example of a glue file (this is the one that maps to the C/C++ "stdio" library).

```
#include <stdio.h>

#define INI_FILETYPE                  FILE*
#define ini_openread(filename,file)   ((*(file) = fopen((filename),"r")) != NULL)
#define ini_openwrite(filename,file)  ((*(file) = fopen((filename),"w")) != NULL)
#define ini_close(file)               (fclose(*(file)) == 0)
#define ini_read(buffer,size,file)    (fgets((buffer),(size),*(file)) != NULL)
#define ini_write(buffer,file)        (fputs((buffer),*(file)) >= 0)
#define ini_rename(source,dest)       (rename((source), (dest)) == 0)
#define ini_remove(filename)          (remove(filename) == 0)

#define INI_FILEPOS                   fpos_t
#define ini_tell(file,pos)            (fgetpos(*(file), (pos)) == 0)
#define ini_seek(file,pos)            (fsetpos(*(file), (pos)) == 0)
```

As you can see, a glue file is mostly a set of macros that wraps one function definition around another.

The glue file may contain more settings, for support of rational numbers, to explicitly set the line termination character(s), or to disable write support (for example). See the manual that comes with the archive for the details.