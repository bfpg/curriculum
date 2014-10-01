Lists
=====

So far, we've dealt with discrete pieces of data: one number, one
string, one value.  When programming, it is more often the case that
you want to work with multiple values.  Haskell has many types for
working with collections of values.  Such types are commonly called
_data structures_, and one such type is the _list_.

Lists are sequences of zero or more values of a single type.  Let's
look at some lists.

```haskell
listOfInt :: [Int]
listOfInt = [1, 2, 3, 5, 5]

listOfBool :: [Bool]
listOfBool = [True]

emptyList :: [Bool]
emptyList = []
```

List _types_ are just the type that the list contains wrapped in
square brackets, e.g. `[Integer]`.  List _values_ are also wrapped
in square brackets, but contain a comma-separated list of values, or
for the empty list, nothing at all.

Under the hood, lists are actually put together with the `(:)`
function (pronounced "_cons_", for _construct_).  The following
expressions are equivalent:

```haskell
[1,  2,  3,  4,  5]
(1 : 2 : 3 : 4 : 5 : [])
```

`(:)` takes one value and glues it to the front of a _list of
values_ of the same type.  This is why the second expression has the
empty list at the end.

# Working with lists

What can you do with lists?  There are functions for reversing
lists, appending lists, filtering lists, and many more!  You can
write your own list functions.  Let's write a function to calculate
the sum of a list of `Integer`.

```haskell
sumIntList :: [Int] -> Int
sumIntList []     = 0
sumIntList (x:xs) = x + sumIntList xs
```

The `sumIntList` function has two _patterns_: one for the empty
list (`[]`) case, and one for non-empty list.  You can see `(:)`
used in the second pattern to separate the _head_ of the list (which
we have called `x`) and the _tail_ (called `xs`).

As you would expect, `sumIntList` for an empty list is defined as
`0`.  If the list is non-empty, to compute the sum we add the head
of list (`x`) to the sum of the rest of the list (`sumIntList xs`).
This concept of applying a function within its own definition is
called _recursion_.


# Generic list functions

Let us consider a function to calculate the length of a list:

```haskell
lenIntList :: [Int] -> Int
lenIntList []     = 0
lenIntList (x:xs) = 1 + lenIntList xs
```

This function defines the length of an empty `[Int]` as `0`, and the
length of a non-empty list is defined as `1` plus the length of the
tail of that non-empty list.

But what if we had a `[Bool]` instead of a `[Int]`?  We do not want
to write what is essentially the same function multiple times for
different types.

If the type of the values insides the list doesn't matter - for
computing the length of a list, it doesn't - we can put a _type
variable_ in the type signature, instead of a _concrete type_ like
`Int` or `Bool`.

```haskell
len :: [a] -> Int
len []      = 0
len (x:xs)  = 1 + len xs
```

The type variable `a` is a promise that this function will work for
any type.  So only one function for calculating the length of a list
needs to be written, and it will work for any conceivable list.


### EXERCISE: Make a list

Make a list of the high temperatues for the next 7 days in the town
where you live.  Write a function to calculate the average high for
the week.
