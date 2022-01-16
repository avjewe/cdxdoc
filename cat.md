# cat : Concatenate Files
USAGE : `cdx cat [options...] [files...]`

Combine files, one after the other. Do the right thing with file headers.

## Command Line Options

||||
|---|---|---|
|-h|--header=Mode|Header requirements. See below.|
|-p|--pad=Mode>|Add trailing newline if absent. See below.|
|-n|--number=Name\[,Start\[,Where]]|Number the lines in column 'Name', starting at number 'Start', 'Where' can be 'begin' or 'end'|
|-b|--begin|Shortcut for `--number number,1,begin`|
|-e|--end|Shortcut for `--number number,1,end`|
|-r|--remove=[Matcher](Matcher.md)|Remove lines that match. Most useful matchers are: Empty, Blank, Hash, Slash|
|-s|--skip=[Matcher](Matcher.md)|Do not number lines that match.|


### Header Mode
The header mode dictates what file headers are expected, and what to do when files don't match each other
 * Match -- First file can be anything, all other files must match the first one. This is the default.
 * Require -- All files must have identical CDX headers
 * Strip -- Strip CDX headers if present
 * None -- The presence of a CDX header is an error
 * Trust -- Strip CDX headers from all but first file. Trust that the data is compatible.
 * Ignore -- Treat CDX Headers just like any other line of data

### Pad Mode
What to do if files don't end with a newline
 * Yes - Always append a newline if one isn't present.  This is the default.
 * No - Never append a newline.
 * End - Appen a newline to the last file, if necessary. 
 
[home](README.md)
