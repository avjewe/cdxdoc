Aggregators turn many values into one value. Primarily used in [uniq](uniq.md), where they are associated with an input and output column.

Syntax is Method,Pattern. Available methods include :

* count       The number of things aggregated
* prefix      The longest common prefix of the input values
* suffix      The longest common suffix of the input values
* min,comp    Keep the minimum value, Pattern is the associated [Comparator](Comparator.md)
* max,comp    Keep the maximum value, Pattern is the associated [Comparator](Comparator.md)
* mean        The arithmetic mean of the values
* sum         The sum of the values
* merge       Merge into a delimited list of values

The pattern for a `merge` aggregator is a period delimited set of any of the following :
* sort        --  sort the parts
* uniq        -- Remove any adjacent equal parts. Happens after sorting.
* count       -- Display the count of parts, not the parts themselves.
* max_len:N   -- Discard any parts longer than N bytes.
* min_len:N   -- Discard any parts shorter than N bytes.
* max_parts:N -- Display only the first N parts.
* Dxy         -- 'x' is the input delimiter and 'y' is the output delimiter. Default is comma for both.
* comp:spec   -- Spec for comparator for sort or uniq. Must be last piece.

[home](README.md)
