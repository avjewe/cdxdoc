A matcher looks at some text, in the context of a pattern, and states `yes` or `no` : that text matches this pattern.

A matcher is specified with a period delimited list, consiting of a method and some modifiers.
An empty specification indicated a case sensitive regex over plain bytes.

A matcher is commonly used as a single comma delimited parameter : `Matcher,Pattern` (e.g. [cat](cat.md)) or `Column,Matcher,Pattern` (e.g. [cgrep](cgrep.md)).
In both cases it's fine for the Pattern to contain commas. Modifers and methods are not case sensitive.

 ## Modifiers :
 
    * utf8 - String : operations are on utf8 strings, rather than the default u8 bytes
    * not - Negate : treat a match as a non-match, and vice versa.
    * case - Case Insensitive : ignore case. Exact behavior depends on "S"
    * trim - remove leading and trailing whitespce before checking
    * null - an empty string also matches. This check happens after trimming.
    * and - See Multi-Match below. Matches if all pattern match.
    * or - See Multi-Match below. Matches if any pattern matches.
    
If you do not specify 'S' in the modifiers, then matching against non-utf8 field values is OK. 
 

 ## Methods :
 
    * regex - A regex as per the eponymous crate
    * exact - An exact match
    * prefix - The pattern is a prefix of the field value
    * suffix - The pattern is a suffix of the field value
    * infix - The pattern is a contained in the field value.
    * file-exact - The pattern is a file name. The field value exactly matches one of the lines in the file.
    * glob - The pattern is a shell-style glob pattern, like `*.txt`
    * length - The pattern is either one number, or two comma delimited numbers. The first number if the minumim string length, the second is the inclusive maximum.
    * empty - Matchs only the empty string. Pattern is ignored. The same as `length` if you specified `0,0` as the pattern.
    * blank - Matches a string composed enirely of whitespace. A superset of `empty`.
    * hash - Matches a string starting with whitespace, followed by `#`. Pattern is ignored. A superset of `blank`.
    * slash - Matches a string starting with whitespace, followed by `//`. Pattern is ignored. A superset of `blank`.
    * yes - Always matches. Use `yes.N` for something that never matches.
    
## Multi-Match
A normal match is `Matcher,Pattern`

A multi-match contains multiple patterns. If the Modifiers contains `AND` or `OR`, then the first character of the pattern is interpreted as a delimiter, and the Pattern string is split on that delimiter, into multiple patterns. e.g.
`c.or.regex,,Pattern,Pattern,Pattern` or `Column,AND,^Pattern^Pattern^Pattern`

