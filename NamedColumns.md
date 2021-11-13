# Dedicated header line to name columns

cdx can handle text files with a special header line. 

This line starts with " CDX&lt;delim>", that is a space, the letters CDX, and the column delimiter used in the file.

That tag is followed by the column names, delimited by the given delimiter.
Column names must start with an alphabetic character which is then followed by one or more alphanumeric characters or underscores. 

So Legal names include "title" "the_author" "x" and "X_12345"

Illegal names include "7" "\_title" "the-author"

A header line is malformed if it contains multiple columns that share the same name.

### Named Column

When a tool asks for a column, you can use a name or number, e.g. "7" or "title"

### Column Set

When a tool asks for a ColumnSet, that is a comma delimited list of Ranges

A Range starts with an options "~" signaling "not", followed by one of
 * a single **Named Column**
 * two named columns, separated by a "-" indicating an inclusive range. The second one can be omitted, meaning "all the rest"
 * A comparison operator, followed by a string, e.g. "<abc" or ">=def", include all columns matching (case sensitive) the given expression
 * Two such comparisons, e.g. ">=abc<def" selecting any columns that are alphabetically between "abc" and "def".
 * A bash-style glob, e.g. "t*e" or "ti???", both of which would match the column "title" among others.

The full column set then represents all the regulat ranges, in order, with any and all not'ed column removed.

This means that repeating a "yes" column is significant, but repeating a negated column changes nothing. For example

* `1,3,5` - columns 1, 3 and 5
* `1-3,5` - columns 1,2,3 and 5
* `1-5,~3` - columns 1,2,4,5
* `1-` - all the columns
* `1,1,2,2` - column 1, column 1 again, column 2, column 2 again
* `~2-3,1-5,~3-4` - columns 1 and 5

### Scoped Value

A scoped value lets you specify a value that is potentiall different for every column. It is a value followed by a comma followed by a **Column Set**. These can be specified multiple times, to give different values to different columns. If the same column is given multiple values, the rightmost one on the command line take priority. If no comma is present, the vthe alue applies to all columns. For example, if the command like option is "-s", and assuming 5 columns,

 * `-s foo` --  columns 1-5 get "foo"
 * `-s foo -s bar,2-4` -- column1 1 and 5 get foo, 2-4 get bar
 * `-s ,,3` -- column 3 gets ","
 * `-s foo,~2-4` -- columns 1 and 5 get foo.


