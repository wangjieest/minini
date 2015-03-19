**Note**: this project is now on Github. Please go to https://github.com/compuphase/minIni for the latest changes. Stable versions will be released on http://www.compuphase.com/minini.htm when they become available.

---


minIni is a portable and configurable library for reading and writing ".INI" files. At 830 lines of commented source code (version 1.2), minIni truly is a "mini" INI file parser, especially considering its [features](minIni_Features.md).

The library does not require the file I/O functions from the standard C/C++ library, but instead lets you [configure the file I/O interface](Filesystem_Adaption.md) to use via macros. minIni uses limited stack space and does not use dynamic memory (malloc and friends) at all.

Some minor variations on standard [INI files](INI_File_Syntax.md) are supported too, notably minIni supports INI files that lack sections.

The minIni library is based in part on code written by [Joseph Graf](Acknowledgement.md).