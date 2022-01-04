# Verify a file's contents

USAGE : `cdx verify [options...] [files...]`

Run `cdx verify` against your file. Either it prints nothing and returns a zero result code, or it tells you where your
file is wring, and return a non-zero result code.

## Command Line Options

||||
|---|---|---|
|-p|--pattern=Col,[Matcher](Matcher.md),Pattern|This column must match this pattern|
|-k|--key=[Comparator](Comparisons.md) |Sort criterea for the below.|
|-s|--sort|File must be sorted by `--key`|
|-u|--unique|Adjacent lines must not be equal, according to  `--key`. Enables --sort.|
|-f|--first=Op,Value|'FirstLine Op Value' must be true. E.g LT,a for first line is less than 'a'.|
|-l|--last=Op,Value|'LastLine Op Value' must be true. According to --key, of course.|
|-r|--report=Number|Report this many problems before exiting. Default 5.|


[home](README.md)
