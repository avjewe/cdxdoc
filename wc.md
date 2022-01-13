# Count words, lines and characters

USAGE : `cdx wc [options...] [files...]`

|short|long|description|
|---|---|---|
| -a | --agg=NewCol,[Aggregator](Aggregator.md)  | Create a new output column with the given aggregator. |
| -l | --lines | Shortcut for `--agg lines,count` |
| -b | --bytes | Shortcut for `--agg bytes,asum,chars` |
| -c | --chars | Shortcut for `--agg chars,asum,utf8.chars` |
| -w | --words | Shortcut for `--agg words,asum,swords` |
| -f | --file=Tri,ColName | Should we add the filename as the first column? Default is to do so only when there is more than one output line. |
| -h | --header=Tri | Should we add the CDX file header? Default is to do so only when there is more than one column. |
| -t | --total=Tri or `only` | Should we include a line of totals at the bottom? Default is to do so only when there is more than one file. `only` means to print only the total and not the values for individual files |
| -o | --format=NumberFormat | What format should numbers be printed in? |

If no output is specified, `--lines` is assumed.

`wc` reads each line and feeds it to each aggregator.

Best viewed when piped to [cdx tabs](tabs.md)

### Other useful aggregators

* `--agg ,amax,chars.utf8` will report the length of the longest line in characters
* `--agg ,amean,awords` will report the average line length in words

### Number Format
 * Plain : No exponent. e.g. 123456 or 123456789
 * Float : With exponent, e.g. 1.23e5 or 1.23e8
 * p2 : Power of Two suffix, e.g. 121K or 118M
 * p10 : Power of Ten suffix, e.g. 123k or 123m

[home](README.md)

