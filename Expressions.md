# Arithmetic Expressions

Arithmetic expressions in `cdx` support the `math.h` part of the `C` standard library. That is, you get constants such as `M_SQRT2` and functions such as `hypot`. Only the function that return a single floating point number are supported, e.g. not `sincos`

### Operators

Unary Operators : Leading `+` and `-` as well as trailing `!` (factorial)

Binary Operators : The usual `+,-,*,/,%` as well as ^ (power) and the comparison operators `<,<=,>,>=,==,!=` which produce `0.0` if false and `1.0` if true.

### Additonal Functions

* abs() - alias for fabs()
* min - takes any number of arguments (at least one) and returns the minimum
* max - takes any number of arguments (at least one) and returns the maximum
* avg - takes any number of arguments (at least one) and returns the average
* if - takes 3 arguments. If the first is non-zero, returns the second, else returns the third.

# Uses

Expressions are used throughout the cdx tools

* [Comparators](Comparator.md) : e.g. `cdx sort -k ',expr,sin(angle)'` sorts a file by the sin of the value of the 'angle' field.
* [Matchers](Matcher.md) : e.g. `cdx cgrep -e 'price*quantity > 100.0'` selects the line where the `price` column multiplied by the `quantity` column is greater than 100. 

[home](README.md)
