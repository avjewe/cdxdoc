# Select, combine ansd rearrange parts of a line

USAGE : `cdx cut [options...] [files...]`

## Command Line Options

||||
|---|---|---|
|-f|--fields=Columns|the columns to select as a [Column Set](NamedColumns.md)|
|-g|--group=Spec|The columns in a bunch, e.g. '.group:1-3'|
|-c|--composite=Spec|New value made from parts. e.g. 'stuff:abc^{two}def'|

These items will appear in the output file, left to right, in the same order as they were on the command line.

### Group Spec
A group is a collection of input columns, squashed together into a single output column. The spec format is
1. A single byte delimiter
2. The name of the new column (can be empty of output has no column names) followed by a colon.
3. A [Column Set](NamedColumns.md) specifying the columns to be used

### Composite Spec
A composite column combines input columns with literal text into a single output column. The spec format is "Name:" specifying the name of the new column followed by a string containg any number of ^{Column} identifiers, mixed up with litera text.
