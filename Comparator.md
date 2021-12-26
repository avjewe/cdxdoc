# How to compare two lines

Many cdx tools need to compare lines of text with each other, for sorting or just equality.

The default behavior is a simple textual match of the whole line - byte for byte.

These tools can take a Comparator of the form `--key=Spec` where the spec is :

Columns,Method,Pattern

where Column is a column name or number. Leave this empty to look at the line as a whole, or for comparators like `expr` that
do not need a separate column specification. Most comparators don't take a pattern, so you can simplify to simply
`Column,Method`. The default method is `plain`, so for a plain comparison, you can simplify to `Column`. An empty string
would compare the whole line, plain.

By default, a field that does not represent a valid value for the method sorts higher than any valid value,
but by default, all field values are considered valid. 

Method is one of :

 * plain : sort the plain bytes of the column (the default)
 * expr : sort the value of the arithmetic expression in the pattern.
 * length (or 'len') : sort fields by their length
 * float : best effort to convert field to 64-bit floating point value, and compare that
 * numeric (or 'num') : Numeric compare, assuimg input is in the form [-]nnn.nnn, with no limit on length or value
 * ip : Sort as IP address or 1.2.3 section numbers
 * lower : Sort as lower case ascii
 * equal : All lines are always equal to each other

Combined with :

* rev : reverse sort
* low : invalid values sort lower than any valid value
* trail : a valid value with trailing garbage is ok. That is, a value is invalid unless it has a valid prefix.
* strict : All bytes of the field must contain a valid value

For example

 * `--key 2` sorts by column 2 increasing.
 * -k price,float.strict
 * `-k 3,rev.float` sorts by column 3, by decreasing floating point value
 * `--key title,rev.len` sorts by decreasing length of the title column
 * `-k author -k title` sorts by author, and if the authors are the same, by title.
