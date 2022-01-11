# Name Columns and how to use them

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

A Range starts with an optional "Name:", giving a new name to the column, followed by a optional "~" signaling "not", followed by one of
 * a single **Named Column**
 * two named columns, separated by a "-" indicating an inclusive range. The second one can be omitted, meaning "all the rest"
 * a [Matcher](Matcher.md) inside parentheses, which selects any columns whose name matches the Matcher, e.g. `(range,<=dog>=cat)`

The full column set then represents all the regular ranges, in order, with any and all not'ed column removed.

This means that repeating a "yes" column is significant, but repeating a negated column changes nothing. For example

* `1,3,5` - columns 1, 3 and 5
* `1-3,5` - columns 1,2,3 and 5
* `1-5,~3` - columns 1,2,4,5
* `1-` - all the columns
* `1,stuff:1` - column 1 with its original name, column 1 again but with the column name "stuff"
* `~2-3,1-5,~3-4` - columns 1 and 5

### Scoped Value

A scoped value lets you specify a value that is potentiall different for every column. It is a value followed by a comma followed by a **Column Set**. These can be specified multiple times, to give different values to different columns. If the same column is given multiple values, the rightmost one on the command line take priority. If no comma is present, the vthe alue applies to all columns. For example, if the command like option is "-s", and assuming 5 columns,

 * `-s foo` --  columns 1-5 get "foo"
 * `-s foo -s bar,2-4` -- column1 1 and 5 get foo, 2-4 get bar
 * `-s ,,3` -- column 3 gets ","
 * `-s foo,~2-4` -- columns 1 and 5 get foo.

### Transforms

A column set can be followed by a `+` and a [Transform](Transform.md) chain, for example `1-3+lower+to_base64`.
This will give you the values of those fields, each individually transformed as requested.
