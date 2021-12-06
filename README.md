# Documentation for the rust cdx package.

The cdx application is something like the gnu textutils, with added benefits :

* Written in Rust
* Generally faster, and better at dealing with enormous files
* Supports [Named Columns](NamedColumns.md)
* Supports a wide variety of [Comparators](Comparator.md) and [Matchers](Matcher.md)
* Supports [File Magic](FileMagic.md)

Tools
* [cat](cat.md) Concatenate files.
* [binsearch](binsearch.md) Search in sorted files.
* [cgrep](cgrep.md) Select lines from a file, based on matching column values.
* [cut](cut.md) Select combine and rearrange parts of each line.
* [join](join.md) Join files on a matching column.
* [sort](sort.md) Sort the lines of a set of input files.
* [tooltest](tooltest.md) Test command line tools.
* [uniq](uniq.md) Select only one of any set of adjacent lines.

The SQL query
`SELECT table1.title,table2.author from tabel1 JOIN table2 ON table1.id == table2.id WHERE tabel1.mode == "avail"` can be translated as

`cdx cgrep -p, mode,,avail table1.txt | cdx join -k id - table2.txt -o 1.title,2.author` 
