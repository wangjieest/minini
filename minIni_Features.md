minIni is a programmer's library to read and write "INI" files in embedded systems. minIni takes little resources, can be configured for various kinds of file I/O libraries and provides functionality for reading, writing and deleting keys from an INI file.

Although the main feature of minIni is that it is small and minimal, it has a few other features:
  * minIni supports reading keys that are outside a section, and it thereby supports configuration files that do not use sections (but that are otherwise compatible with INI files).
  * You may use a colon to separate key and value; the colon is equivalent to the equal sign. That is, the strings "Name: Value" and "Name=Value" have the same meaning.
  * The hash character ("#") is an alternative for the semicolon to start a comment. Trailing comments (i.e. behind a key/value pair on a line) are allowed.
  * Leading and trailing white space around key names and values is ignored.
  * When writing a value that contains a comment character (";" or "#"), that value will automatically be put between double quotes; when reading the value, these quotes are removed. When a double-quote itself appears in the setting, these characters are escaped.
  * Section and key enumeration are supported.
  * You can optionally set the line termination (for text files) that minIni will use. (This is a compile-time setting, not a run-time setting.)
  * Since writing speed is _much_ lower than reading speed in Flash memory (SD/MMC cards, USB memory sticks), minIni minimizes "file writes" at the expense of double "file reads".
  * The memory footprint is deterministic. There is no dynamic memory allocation.

# INI file reading paradigms #

There are two approaches to reading settings from an INI file. One way is to call a function, such as `GetProfileString()` for every section and key that you need. This is especially convenient if there is a large INI file, but you only need a few settings from that file at any time --especially if the INI file can also change while your program runs. This is the approach that the Microsoft Windows API uses.

The above procedure is quite inefficient, however, when you need to retrieve quite a few settings in a row from the INI file --especially if the INI file is not cached in memory (which it isn't, in minIni). A different approach to getting settings from an INI file is to call a "parsing" function and let that function call the application back with the section and key names plus the associated data. XML parsing libraries often use this approach; see for example [the Expat library](http://expat.sourceforge.net/).

minIni supports both approaches. For reading a single setting, use functions like `ini_gets()`. For the callback approach, implement a callback and call `ini_browse()`. See the minIni manual for details.