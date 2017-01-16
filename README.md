bash_ini_parser -- Simple INI file parser
=========================================

This is a comfortable and simple INI file parser to be used in bash scripts.

License
-------

This software is provided under the BSD license.  The text of this license
is provided below:

--------------------------------------------------------------------------

Copyright (C) 2009 Kevin Porter / Advanced Web Construction Ltd
Copyright (C) 2010-2014 Ruediger Meier
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions
are met:

1. Redistributions of source code must retain the above copyright
   notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright
   notice, this list of conditions and the following disclaimer in the
   documentation and/or other materials provided with the distribution.

3. Neither the name of the author nor the names of any contributors
   may be used to endorse or promote products derived from this
   software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE AUTHOR "AS IS" AND ANY EXPRESS OR
IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED.  IN NO EVENT SHALL THE REGENTS OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR
BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE
OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN
IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

Usage
-----

You must source the bash file into your script:

```bash
. read_ini.sh
```

and then use the read_ini function, defined as:

```bash
read_ini INI_FILE [SECTION] [[--prefix|-p] PREFIX] [[--booleans|b] [0|1]]
```

If SECTION is supplied, then only the specified section of the file will be processed.

After running the read_ini function, variables corresponding to the ini file entries will be available to you. Naming convention for variable names is:

```bash
PREFIX**__SECTION__**VARNAME
```

PREFIX is 'INI' by default (but can be changed with the --prefix option), SECTION and VARNAME are the section name and variable name respectively.

Additionally you can get a list of all following informations:
* **PREFIX__ALL_VARS** : list of variables,
* **PREFIX__ALL_SECTIONS** : list of sections,
* **PREFIX__NUMSECTIONS** : number of sections. 

For example, to read and output the variables of this ini file:

```bash
var1="VAR 1"
var2 = VAR 2

[section1]
var1="section1 VAR 1"
var2= section1 VAR 2
```

you could do this:
```bash
. read_ini.sh

read_ini test1.ini

echo "var1 = ${INI__var1}"
echo "var2 = ${INI__var2}"
echo "section1 var1 = ${INI__section1__var1}"
echo "section1 var2 = ${INI__section1__var2}"

echo "list of all ini vars: ${INI__ALL_VARS}"
echo "number of sections: ${INI__NUMSECTIONS}"
```

Options
-------

**[--prefix | -p] PREFIX**
String to prepend to generated variable names (automatically followed by '__').
*Default: INI*

**[--booleans | -b] [0|1]**
Whether to interpret special unquoted string values 'yes', 'no', 'true',
'false', 'on', 'off' as booleans.
*Default: 1*

Ini file format
---------------

- Variables are stored as name/value pairs, eg:
```bash
var=value
```

- Leading and trailing whitespace of the name and the value is discarded.

- Use double or single quotes to get whitespace in the values

- Section names in square brackets, eg:
```bash
[section1]
var1 = value
```

- Variable names can be re-used between sections (or out of section), eg:
```bash
var1=value
[section1]
var1=value
[section3]
var1=value
```

- Dots are converted to underscores in all variable names.

- Special boolean values: unquoted strings 'yes', 'true' and 'on' are interpreted as 1; 'no', 'false' and 'off' are interpreted as 0

