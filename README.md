# JZON
An offshoot of the JSON specification prioritizing easier human editing and ease of implementation.

Specific example implementation focus's on a small memory foot print, detailed logging, and high speed processing input.

**Uses Zig 0.10.0.**

# Why Not Json?
Json, is insanely simple. Insanely human readable, ***mostly*** well defined besides a few edge cases which 
is the explicit purpose for JZON. The whole point is to add a nice simple and clean update for json to fix the tiny things,
while still being able to parse original json files and specifiying the interface coders interact with after parsing.

# Why Not Use A JSON Library?
My stance is doing it yourself is always better as an educational experience. That's how I like to do it and that's
the way I'm going to do it until I've reached a point where it would be too much work. ( Something like supporting png
and jpeg without using common libraries. )

# What Are The Differences?
- Array's and Objects can end with a comma. IE. [ 9 , 5 , 3 ,] { 9, 5, 3, }
- Objects can be indexed with or without key. ( Preferably indexed without as that's always faster )
- Array's are EXPLICITELY required to be all the same type of value because they will be stored as a literal array in memory.
  ( Multidimensional arrays will not due to complexity of implementation, a single array will be continous though, and techinically they are oriented properly but the functionality isn't really that crucial to me )
- MultiDimensional array's are EXPLICITELY required to have each array inside of it be the same length, again because that is how it will be layed out in memory.

# Specification

Everything in JZON is a value of some type.

There are objects, which hold values of variable length and variable types. The values can just be indexed by order of placement like an array but still require keys like json ( .getFromKey(), .getFromIndex() ).

There are arrays, which are of variable length with EACH VALUE INSIDE BEING THE SAME TYPE. When the JZON struct contains an array, you must run the function ".getArray()" to return a pointer to the const memory of the array.

There are "simple-values" that can't hold other values, things like numbers ( int, float, hex turned into int, or exponent to float ), strings, bools, and null.

A number's type is inferred and given the largest type commonly allowed ( f64, i64 ).

Comments are allowed and are designated by "//". Comments go until they find a new line, and are treated as whitespace.

Jzon parsers can read Json, but not the other way around.
The supported types are-

i64
f64
string
bool
null
object
array
