# uniq : Select only one of any set of equivilent adjacent lines.

USAGE : cdx uniq [options...] [file]

### Command Line Options

| short | long | description |
|---|---|---|
| -k | --key **_Spec_** | How to compare adjacent lines. Spec is any of the standard [Comparisons](Comparisons.md) |

If any adjacent lines compare equal, only the first is printed.


