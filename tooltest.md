# Test command line tools

USAGE : `cdx tooltest [options...] [files...]`

cdx tooltest takes test files, runs the associated commands, and reports success or failure.

## Command Line Options

||||
|---|---|---|
|-b|--bin=Dir|Location of executables to test|
|-t|--tmp=Dir|Use this for the temporary directory, and do not delete the temporary files|

A tooltest file specifies a command, some input files, and some output files. It creates the input files, runs the command, and verifies that the output files are as they should be. It also verifies the result code.

## Output Files

A test can specify any number of output files, and the test will fail if any additional files are created.

Output files (i.e. #stdout, #stderr and #outfile) can be specified in two ways

### Exact Contents
```
#stdout
foo
bar
```
says that stdout should have exactly those eight bytes. The file format requires that this ends with a newline, so use
```
#stdout
foo
bar
#nonewline
```
to indicate that the final newline is NOT expected in the output.

### [Matcher](Matcher.md)

Specify a matcher, and the test will pass if the file contents matches. This is most useful with #stderr, where you don't want the tests to break if the error message changes, but you want some sanity checking. For example,
```
#stderr substr.and.C,,duplicate,one
```
says that the stderr output should contain both the word "duplicate" and the word "one", thus matching either "Column name 'one' is a duplicate" and "Duplicate column name : one".

Remember that if you're using a `regex` matcher, you need to include `(s?)` in the pattern if you want a match to cross a line boundary.

## File Format
A tooltest file (traditionally with a `.test` suffix) has the following parts. All but `command` are optional

 * #command CMD : the command to be run
 * #stdin : followed by the input to the program. Default empty.
 * #stdout : followed by the expected stdout output. Default empty.
 * #stderr : followed by the expected stderr output. Default empty.
 * #infile Filename : followed by the contents of the named file. `#infile foo` means that the file $TMP/foo is available to the command.
 * #outfile Filename : followed by the contents of the named file. `#outfile foo` means that the file $TMP/foo must be created by the command, with exactly that contents.
 * #nonewline : must follow the contents of one of the above four. Removes the final newline from the input or expected output.
 * #status Number : the expected exit status. Default zero.
 * '# ' : a line starting with # and a space is a comment, and is ignored

## Temporary Directory

Normally, tooltest will create a temporary directory, and delete it when it's done. If you use `--tmp` to specify a directory,
1) the directory will be created, if it does not exist
2) files will be written to that directory, including `stdin` `stdout` and `stderr`
3) these files will NOT be deleted
4) tooltest will NOT check for extranious outout files.

This is intended to be used for only a single test, for use in debugging, see below.

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

Files are created in a temporary directory, so on the command line, you must explicitly refer to that directory :

```
#command cdx cat $TMP/aaa.txt $TMP/bbb.txt
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

## Debugging

Under normal circumstances, you'll run something like `cdx tooltest -b target/debug test/*.test` as part of your build, and usually if a test fails, it's that line of code you just changed.

If the failure is more confusing, you should 

 1) run `cdx tooltest --tmp foo -b target/debug test test/ThatOneTest.tst`. This will report, among other things `Test test/ThatOneTest.tst failed MyApp arg1 arg2`
 2) `cd foo`
 3) examine output files,
 4) run `MyApp arg1 arg2 < stdin` in the debugger, or with extra eprintln!'s 


[home](README.md)
