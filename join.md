# Join Files on matching column
`cdx join [options...] file_1 file_2

## Command Line Options
||||
|---|---|---|
|-a|--also=**_FileNum_**,**_FileName_**|Write non-matching lines from this file to this file.|
|-f|--file=**_FileName_**|Write matching lines to this file, default is "-" for stdout|
| -k | --key **_Spec_** | How to compare adjacent lines. Spec is any of the standard [Comparisons](Comparisons.md) |
|-o|--output=Spec|Output Columns. See below.|

Output Columns are a comma delimited list of [Column Sets](NamedColumns.md). 

The first item in the list must be prefixed with a file number, followed by a period, e.g. `1.2` refers to the second column of the first file.

Other items in the list may be prefixed by a file number. If not, the previously specified column number is assumed, e.g. `2.1-3,~2,1.3,1.1` indicates
columns 1 and 3 from the second file, followed by columns 3 and 1 from the first file. `-o 1.1,2.2` is the same as `-o 1.1 -o 2.2`.
