# How to compare two lines

Many cdx tools need to compare lines of text with each other, for sorting or just equality.

The default behavior is a simple textual match of the whole line - byte for byte.

These tools can take a Comparator of the form `--key=Spec` where the spec is :

Column:Mode

where Column is a column name or number. If a number, then the colon is optional. 

Mode is one of :

 * L : sort fields by their length
 * g : best effort to convert field to floating point value, and compare that
 * : default is regular text compare

Combined with :

* r : reverse sort

For example

 * `--key 2` sorts by column 2 increasing.
 * `-k 3gr` sorts by column 3, by decreasing floating point value
 * `--key title:rL` sorts by decreasing length of the title column
 * `-k author -k title` sorts by author, and if the authors are the same, by title.
