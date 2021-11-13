# Test command line tools

USAGE : `cdx tooltest [options...] [files...]`

cdx tooltest takes test files, runs the associated commands, and reports success or failure.

## Command Line Options

||||
|---|---|---|
|-b|--bin=Dir|Location of executables to test|

## File Format
A tooltest file (traditionally with a `.test` suffix) has the following parts. All but `command` are optional

#command CMD : the command to be run
#stdin : followed by the input to the program. Default empty.
#stdout : followed by the expected stdout output. Default empty.
#stderr : followed by the expected stderr output. Default empty.
#infile Filename : followed by the contents of the named file. FIle name must be prefixed with `$TMP` in the command.
#nonewline : must follow the contents of one of the above four. Removes the final newline from the input or expected output.
#status Number : the expected exit status. Default zero.
'# ' : a line starting with # and a space is a comment, and is ignored

## Examples
The best place to find examples is in the [cdxtest](https://github.com/avjewe/cdx/tree/main/cdxtest) directory of the git repo.
```
#command cdx cut -f two
#stdin
 CDX  one two three
this  that  other
aaa bbb ccc
#stdout
 CDX  two
that
bbb
```


```
#command cdx cat aaa.txt bbb.txt
#infile aaa.txt
 CDX  one two
this  that
#infile bbb.txt
 CDX  one two
aaa bbb
#stdout
 CDX  one two
this  that
one two
```
