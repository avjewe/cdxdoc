# uniq : Select only one of any set of equivilent adjacent lines.

USAGE : cdx uniq [options...] [file]

### Command Line Options

||||
|---|---|---|
| -k | --key **_Spec_** | How to compare adjacent lines. Spec is any of the standard [Comparisons](Comparisons.md) |
|-c|--count=ColName,Position|Add count of matched lines. See below.|
|-w|--which=Pos,Comp|Which of the matching lines is displayed? See below.|
|-a|--agg=Spec|Merge values from this column, in place. See below.|
||--agg-pre|Merge values from this column, into new column. See below.|
||--agg-post|Merge values from this column, into new column. See below.|
||--agg-help|Print help for [Aggregators](Aggregator.md)|

If any adjacent lines compare equal, only the first is printed.

### Count
Count takes a two part, comma delimited parameter. The first part is th new column name, which defaults to 'count'. The second part is 'begin' or 'end', saying that th new column should either be first or last in the output file. The defaul is 'begin', so `-c ,` will produce a new first column named 'count', and `--count Num,End` will produce a new final column named 'Num'.

### Which
When several line are equal (according to `--key`) which line is printed?
 * First -- The first line encountered. This is the default.
 * Last  -- The last line encounteder.
 * Min,Spec -- The line with the minimum value accoring to this [Comparator](Comparator.md)
 * Max,Spec -- The line with the maximum value accoring to this [Comparator](Comparator.md)

### Aggregators
Sometimes you don't want to select one representitive line, but rather you need tom aggregate the values from the input column values into a new
column value. There are three ways to specify aggregation
 * `--agg` replace a column with its aggregate. It is an error to specify the same column twice in this way. The format is `SrcCol,Spec` where `SrcCol` is the column to be aggregated and `Spec` is the desired [Aggregator](Aggregator.md)
 * `--agg-pre` Create a new column, placed before the columns of the input file. The format is `NewCol,SrcCol,Spec` where `NewCol` is the name of the new column, and the rest is as in `--agg`
 * `--agg-post` Just like --agg-pre, but the new column is places after the original columns.

### Details
There can be many different [Comparators](Comparator.md) in opertion at the same time. For example

`cdx uniq --key title,lower --which Max,price,float --agg year,max,numeric`

The lines of the file are compared by the case-insensitve text of the `title` field. Among those lines with matching titles, the line
with the highest `price` is selected, except that the output `year` column will be the latest year mentioned.

