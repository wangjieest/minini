# INI file syntax #

INI files are best known from Microsoft Windows, but they are also used with applications that run on other platforms (although their file extension is sometimes ".cfg" instead of ".ini").

INI files have a simple syntax with name/value pairs in a plain text file. The name must be unique (per section) and the value must fit on a single line. INI files are commonly separated into sections --in minIni, this is optional. A section is a name between square brackets, like "`[Network]`" in the example below.

```
[Network]
hostname=My Computer
address=dhcp
dns = 192.168.1.1
```

In the API and in this documentation, the "name" for a setting is denoted as the _key_ for the setting. The key and the value are separated by an equal sign ("="). minIni supports the colon (":") as an alternative to the equal sign for the key/value delimiter.

Leading a trailing spaces around values or key names are removed. If you need to include leading and/or trailing spaces in a value, put the value between double quotes. The `ini_gets()` function (from the minIni library, see the minIni manual) strips off the double quotes from the returned value. Function `ini_puts()` adds double quotes if the value to write contains trailing white space (or special characters).

minIni ignores spaces around the "=" or ":" delimiters, but it does not ignore spaces between the brackets in a section name. In other words, it is best not to put spaces behind the opening bracket "`[`" or before the closing bracket "`]`" of a section name.

Comments in the INI must start with a semicolon (";") or a hash character ("#"),
and run to the end of the line. A comment can be a line of its own, or it may
follow a key/value pair (the "#" character and trailing comments are extensions
of minIni).

For more details on the format, please see http://en.wikipedia.org/wiki/INI_file.