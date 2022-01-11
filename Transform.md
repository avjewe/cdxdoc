# Transforms -- modifying your column values

A transform turns values into other values. These are usually used in the contet of a ColumnSet, followed by `+` and a Transform,
as in `ColumnSet+Transform`

Transforms can be chained together with a `+`, and so you can have.  `ColumnSet+Transform1+Transform2+Transform3`. 

Such a ColumnSet selects the same columns as before, but produces each value indivually transformed.

Transform syntax is a period delimited list, consisting of zero or more modifiers plus one transform, optionally followed by a comma and a pattern specific to the particular transform.

### Modifiers

* utf8 - interpret the column value as utf8, and then apply the full unicode version. For example `lower` applied to "NÑ" produces "nÑ", whereas 'utf8.lower' applied to the same string yields "nñ".

### Available Transforms

* from_base64 -- decode base64. The pattern indicates the particular settings, e.g. `url` or `binhex`.
* lower -- make lowercase
* to_base64 -- encode base64. The pattern indicates the particular settings, e.g. `url` or `binhex`.
* upper -- mak muppercare
