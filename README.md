# bash-getopt
Examples of parsing command line arguments in BASH

## mk_opt
This script attempts to encapsulate the complicated parts of getopt. All command line options can be specified using a function call.

```bash
	# Table of command line options and their callbacks
	mk_opt "a" "arga"   ":"  "<N>"  "This has a required argument"  "export VALUE_A="
	mk_opt "b" "argb"   "::" "[X]"  "This has an optional argument"
	mk_opt "c" "argc"   ""   ""     "This has no argument" "true #Hacky no-op callback "
	mk_opt ""  "argd"   ":"   "<N>" "This has no shorthand" 
	mk_opt "h" "help"   ""   ""     "Display this help text"
```

This provides parsing and validation, as well as a nice `usage` function.
```
	~/code/bash-getopt$ ./mk_opt --help
	  Usage: mk_opt [options]

	  Purge teams from the database that have been scheduled for deletion.
	  
	  Options:
	     -a --arga <N>    This has a required argument
	     -b --argb [X]    This has an optional argument
	     -c --argc        This has no argument
		--argd <N>    This has no shorthand
	     -h --help        Display this help text
```

### Features
 * Supports long and short parameters (-h and --help)
 * Supports optional argument values
 * Triggers a callback for each parameter provided by the user
 * Consolidates the configuration of parameters into a one-line call for each parameter

### Drawbacks
It may be much simpler to specify the command line options using mk_opt, but the rest of the code is not simpler at all. This approach is probably not worth taking. I'm posting it here merely for reference. A template script should never be this complicated.

### Bugs
_I have no intention of fixing any bugs in this._ I have seen a few oddities;
 * Optional arguments must have `=`.
  ** Bad: `~/code/bash-getopt$ ./mk_opt -argb 2`
  ** Good: `~/code/bash-getopt$ ./mk_opt -argb=2`
 * Providing a value for a parameter that does not allow a value results in misleading errors

