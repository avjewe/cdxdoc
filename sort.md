# Comine the columns of the input files

USAGE : `cdx paste [options...] [files...]`

`paste` combines the first lines of each file, then the second lines, and so on. If you want to combine columns based on a matching key, you want [join](join.md)

|short|long|description|
|---|---|---|
| -e | --end=[Exact,Early,Late]| What to do mif files have different lengths. Default Exact. See below.|
| -l | --last | In **Late** mode, repeat last line of shorteer files. |
| -d | --default=[ScopedValue](NamedColumns.md) | In **Late** mode, use these value as the defaults, rather than the empty string. |
|-D|--dups=[Fail,Allow,Numeric] | What to do if duplicate column names are found. Default is **Fail**. See below. |
|-r|--rename=Old.New,Old.New,...| If the name **Old** is repeated, replace it with **New**. Eah pair is used only once, and all must be used|
|-R|--rename-sloppy|It is not an error is some renames not used.|

### Example
If aaa.txt contains
```
 CDX  one two
aaa bbb
ccc ddd
```
and bbb.txt contains
```
 CDX  three four
111 222
333 444
```
The `cdx paste aaa.txt bbb.txt` would produce
```
 CDX  one two three four
aaa bbb 111 222
ccc ddd 333 444
```

### Headers

The output file has a CDX header if and only if every input file has a CDX header.

### End Mode

By default, all files must be the same length (have the same number of rows) or it is an error.

With `--end Early`, output stops when any file reaches its end.

With `--end Late`, output continues until all files have reched their end. Zero-length column values are used for shorter files, unless `--last` or `--default` are used.

### Duplicate Column Name

When combining files this way, it is easy to find yourself with multi columns having the same name, which is malformed. By default, `paste` will check for this and fail if it occurrs. If you use `--dups Allow` then messages will be written to stderr, but you will be allowed to create a malformed file. With `--dups Numeric` if the column name `foo` appears more than once, then the second time it will be called `foo1`, the third time `foo2` and so on. If you specify `--rename foo,bar` then the second time `foo` appears, it will be changed to `bar`. 


[home](README.md)
