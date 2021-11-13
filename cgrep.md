# Select lines from text files

USAGE `cdx cgrep [options...] [files...]`
# Command Line Options
||||
|---|---|---|
|-p|--pattern=Pattern|Select line where this col matches this pattern.|

Lines are printed if they match all the patterns.

## Patterns
Patterns have three comma delimited parts. The third part can have commas. The parts are :
1. A [Named Column](NamedColumns.md)
2. A period delimited list of modfiers, possibly empty. The dafault is a case sensitive regex matching bytes.
    * S - String : operations are on utf8 strings, rather than the default u8 bytes
    * N - Negate : trat a match as a non-match, and vice versa.
    * C - Case Insensitive : ignore case. Exact behavior depends on "S"
    * regex - a regex as per the eponymous crate
    * exact - and exact match
    * prefix - the pattern is a prefix of the field value
    * suffix - the pattern is a suffix of the field value
    * infix - the pattern is a contained in the field value.
    * file-exact - The pattern is a file name. The field value exactly matches one of the lines in the file.
    * glob - The pattern is a shell-style glob pattern, like `*.txt`
    * length - The pattern is either one number, or two comma delimited numbers. The first number if the minumim string length, the second is the inclusive maximum.
3. The pattern, interpreted as per the modifiers.

If you do not specify 'S' in the modifiers, then non-utf8 field values are OK. 


## Examples
 * `-p title,x{3}` -- matches lines where the title field contains three x's in a row
 * `-p 3,S.N.C.prefix,ñ -- reject lines where column 3 starts with ñ or Ñ
 * `-p 2,length,42` -- match lines where column 2 it at least 42 bytes long
 * `-p 2,length.S,42` -- match lines where column 2 it at least 42 characters long
