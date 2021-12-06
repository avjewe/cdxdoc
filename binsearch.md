# Search in sorted files
USAGE : `cdx binsearch [options...] Key File [files...]`

Search files, one after the other. Files must be sorted. Very fast, even for enormous files.

## Command Line Options

||||
|---|---|---|
|-k|--key=[Comparison](Comparisons.md)|How are the files sorted|
|-h|--header=Mode|Header requirements. See [cat](cat.md) for more details.|
|-s|--sub-delim=Char|If you have a multi part Comparison, this character delimits the parts of the Key|
|-C|--context=Before,After|Print lines of context around matches. See below.|
|-H|--filename=ColName:Parts|Prefix output lines with file name.|

binsearch memory maps each files, and does a binary search to find all the lines that match the key.

### Context Parameter

 * If a single number, that number of lines of context before and after
 * If two comma delimited numbers, the first is the lines of context before, the other is lines after
 * Each of those one or two parts can themselves be two period delimited numbers. If so, the first is the number of lines
 to use for files that match, and the other for files that don't match.
 
 For example, these are all the same
  * -C 2
  * -C 2,2
  * -C 2.2,2.2

`-C 0.1` will print
 * if the key matches any lines, just those lines
 * else the two lines surrounding the place where the key would have been

### filename parameter : ColName:Parts

Adds a new first column, containing the name of the file from whence the output lines originated.

`ColName` is the name of the new column being added.

If `Parts` is zero, the whole file name is printed.
If it is one, then just the leaf name (i.e. the file without any drectories) is used.
Otherwise, if it is `N`, then the last `N` segments of the path are printed.

Both parts are optional. The column name defaults to `filename` and `Parts` to zero. Use and empty string or just a `:` to accept both defaults.

`:1` says "print just the leaf name, in a column called filename"

`foo` says "print th whole file name in a column called foo"


