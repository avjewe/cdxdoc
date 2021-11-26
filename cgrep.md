# Select lines from text files

USAGE `cdx cgrep [options...] [files...]`
# Command Line Options
|short|long|description|
|---|---|---|
|-p|--pattern=Column,[Matcher](Matcher.md),Pattern|Select line where this col matches this pattern.|

Lines are printed if they match all the patterns.

## Patterns
Patterns have three comma delimited parts. The third part can have commas. The parts are :
1. A [Named Column](NamedColumns.md)
2. A [Matcher](Matcher.md)
3. The pattern, interpreted as per the matcher.

## Examples
 * `-p title,x{3}` -- matches lines where the title field contains three x's in a row
 * `-p 3,S.N.C.prefix,ñ -- reject lines where column 3 starts with ñ or Ñ
 * `-p 2,length,42` -- match lines where column 2 it at least 42 bytes long
 * `-p 2,length.S,42` -- match lines where column 2 it at least 42 characters long
