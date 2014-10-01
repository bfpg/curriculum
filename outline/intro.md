Introduction to Programming with Haskell
========================================

* Why Haskell?
* What is Haskell good at?
* What does Haskell look like?
* What is the REPL?
* Simple values
    - Numbers
* Assigning names to values

## Why Haskell?

If you've never programmed before, you may not know that there are
many languages to choose from. Some of the other languages you might
have heard of or will hear of are C, JavaScript, Python, and Java.

So why are we teaching Haskell? It's not as popular as any of those
languages. We're using Haskell because of three qualities it has
that make it an ideal first language to learn--or a great language
to learn in addition to others you might already know:

* Haskell is _simple_. That's not to say it's not powerful; it is.
  The number of concepts you have to know to program in Haskell is
  small, however, and the concepts are easy to grasp.

* Haskell is _all-purpose_. Some languages have a specific focus.
  JavaScript, for example, was traditionally used only in web pages
  (although that's changed somewhat). Objective-C is used mainly for
  iPhone apps.  Haskell is well suited to these purposes and many
  more.

* Haskell is _fun_. That's a matter of opinion, of course, but we
  think it holds true. I hope that during this course you experience
  the joy of seeing a Haskell program come together and do something
  powerful and surprising.

## What is Haskell good at?

So, we said Haskell is all-purpose, and it is. That doesn't mean it
doesn't have strong suits, though.

Haskell is good at _abstraction_, that is, implementing functions
(units of software behaviour) that work across different types of
data, so that you, the programmer, can think in terms of high-level
concepts and avoid repeating yourself too much.

Haskell is good at preventing many kinds of mistakes programmers
make.  Haskell is what is known as a _statically typed_ programming
language, which means that many kinds of errors can be detected and
prevented when the source code (what the programmer writes) is
_compiled_ into the program that the computer actually runs.

Haskell makes it simple to define rich _data types_ that accurately
model real-world information.  As a programmer, this means that you
spend less time worrying about the validity of your data, and more
time doing useful things with the data.


## What does Haskell look like?

Here's an example of a _function_ in Haskell:

```haskell
double :: Integer -> Integer
double n = 2 * n
```

You probably noticed that the first and second lines look quite
different.  The first line is the _type signature_ of the function,
and the second line is the implementation.  We will discuss each
part separately.

The type signature starts with the name of the function: `double`.
Functions should have sensible names, but in Haskell, the type
signature is just as important - if not more so!  The double-colon
separates the function name from the type information, and can be
pronounced "_has the type_".

After the double-colon, we see `Integer -> Integer`, which means
that when this function is applied to one value of the type
`Integer` it computes, or _evaluates_, another value of the type
`Integer`.  In Haskell, arrows (`->`) separate arguments types and
the return type.

Type signatures can contain other kinds of information of
information from what we have just seen, and we will learn about
these other concepts later.

The second line is the implementation of the function.  We see
`double` written again, but this time it is followed by `n`.  This
is a _pattern_ that binds the name `n` to the value of the first
argument (in our case, the only argument).  Then we see the equals
sign.  In many programming langauges, the equals sign represents
assignment of values to variables, but in Haskell it represents
_equality_.  Function implementations are actually _equations_, so
you can pronounce the `=` as "_is defined as_".  Finally, we see
that `double` is defined as `n * 2` (`n` multiplied by two).

### Comments

When we write code, we try to make it as clear as possible.  Doing
so is important because code needs not only to communicate
information to a computer, but to people as well: other
programmers, your co-workers, your future self!

In Haskell, we use types to communicate as much as possible.  *Types
are documentation*.  But in some situations, when Haskell's types
are not enough, you can use _comments_ to convey additional
information.  Comments are annotations in source code that are
ignored by the compiler; they are used to help _people_ understand
your code.

Comments start with two dashes.  Everything from the dashes to the
end of the line is a comment and is ignored by the compiler.  There
is a second comment style supported by Haskell: you can put your
comment in between a `{-` and a `-}`.  When using this alternative
syntax, comments can span multiple lines.

```haskell
{- this is a comment -}

one = 1  -- and so is this
```


## Simple data types

In order to do anything in a programming language, you need have
_values_ to do things with.  Every value has a _type_, and there are
many different types of values.  Let's look at some of the common
types.

### Numeric types

There are several different types of numbers in Haskell.  There are
types for _integral_ or whole numbers - `Int` and `Integer` - and
types for rational numbers - `Float` (a _floating-point_ number) and
`Double` (also floating point, but with _double_ the precision of
`Float`).  There are other numeric types, but these are the most
common.

(In case you were wondering, the difference between `Int` and
`Integer` is that `Int` is _bounded_ whereas `Integer` values are
not.)

In source code, numeric values are written in a fairly
straightforward way:

```haskell
anInteger :: Integer
anInteger = 1

aFloat :: Float
aFloat = 3.14  -- not quite pi
```

Negative values can be expressed by putting a minus sign in front of
the number, but due to a quirk in how the compiler _parses_ the
source code it is often necessary to wrap the number in
_parentheses_, as below:

```haskell
timesNegativeOne :: Int -> Int
timesNegativeOne n = n * (-1)
```


### Arithmetic

In Haskell, arithmetic functions look similar to the mathematical
operations you learned in school.  The following examples are
contrived but demonstrate these functions in action:

```haskell
additionExample         = 1 + 1
subtractionExample      = 2 - 2
multiplicationExample   = 3 * 3
divisionExample         = 4 / 4
```

You might also recall that addition and multiplication have a
different _order of operations_ or _precedence_; multiplication of
values occurs before addition, for example.  So it is in Haskell.
But you can use parentheses to force expressions to be evaluated in
a particular order.

```haskell
equalsSeven   =  1  +  2  *  3
equalsSeven'  =  1  + (2  *  3)  -- same as previous equation
equalsNine    = (1  +  2) *  3   -- force a different order
```


### Other simple value types

The `Bool` type (short for _boolean_) represents "true or false"
data.  Booleans are heavily used in computing for testing logical
scenarios, conditionally executing particular behaviour, and so on.
In Haskell, a value of type `Bool` has either the value `True` or
`False` - there are no other possible values.  The functions `&&`
(pronounced "_and_") and `||` (pronounced "_or_") are used to
evalute whether two `Bool` values are both `True`, or whether either
of them is `True`, respectively.  The `not` function can be used to
negate a boolean value.

```haskell
andExample1 = True && False   -- False
andExample2 = True && True    -- True
orExample1  = False && True   -- True
orExample2  = False && False  -- False
```

The `Char` type represents textual _characters_.  Some other
languages have a character type with 256 possible values, but
Haskell's `Char` type represents Unicode code points.  Literal
`Char` values are written between single-quotes. All of the
following are valid `Char` values:

```haskell
aLetter      = 'a'
aDigit       = '1'
aGreekLetter = 'λ'
```

The `String` type represents sequences of `Char` values.  String
values appear between double-quotes.  To include a literal
double-quote in a string, _escape_ it with a backslash.  Escapes can
also be used to represent other special characters, including
newlines and tab-stops.

```haskell
aString                 = "Hello, world!"
aStringWithDoubleQuotes = "The cow says \"moo!\""
aTwoLineString          = "First line.\nSecond line."
```

## GHCi

GHCi is an interactive (that's what the _i_ stands for) interface to
Haskell.  (_GHC_ refers to the _Glasgow Haskell Compiler_.) Many
programming languages have a way to evalute code interactively and
Haskell is no exception.  GHCi lets you load modules, inspect types
and definitions, evalute expressions, and more!

Let's fire up GHCi and explore some of its features.  Run `ghci` in
your terminal to begin.  You will see some output followed by a
prompt, similar to the following:

```
% ghci
GHCi, version 7.8.3: http://www.haskell.org/ghc/  :? for help
Loading package ghc-prim ... linking ... done.
Loading package integer-gmp ... linking ... done.
Loading package base ... linking ... done.
Prelude> 
```

If you type an expression at the prompt, GHCi will evaluate it and
print the result.  Try typing a simple arithmetic expression such as
`10 * 10` and see the results.

```
Prelude> 10 * 10
100
```

OK, so you can use GHCi as a calculator.  What else can it do?  We
can use the `:type` command (or its shorthand, `:t`) to ask GHCi to
tell us the type of an expression:

```
Prelude> :type even
even :: Integral a => a -> Bool
```

Whoa, what is going on there?  What is that strange double arrow?
You can ignore it for now, and focus on the familiar parts of the
type signature.  One could read this type signature in the following
way: `even` is a _function_ that is _applied_ to one _Integral_
argument and returns a `Bool` (`True` or `False`).

We can use another GHCi command, `:info` (or `:i`), to find out more
about this `Integral` thing:

```
Prelude> :i Integral
class (Real a, Enum a) => Integral a where
  ...
        -- Defined in ‘GHC.Real’
instance Integral Integer -- Defined in ‘GHC.Real’
instance Integral Int -- Defined in ‘GHC.Real’
```

GHCi has told us that `Integral` is a _class_ with several functions
(omitted for brevity) and two _instances_: `Int` and `Integer`.  You
will learn more about _type classes_ later, but even without a
complete understanding, thanks to the useful information GHCi
emitted you might have inferred that `even` is a function that takes
a whole number and tells us (by way of its `Bool` return type)
whether or not it is an even number.


### Let bindings

When you are working in GHCi you might need to use a particular
_expression_ in multiple places.  It would be frustrating to write
the expression over and over again, so there is a construct for
binding _names_ to expressions.  In this example we use the `let`
keyword to bind the name `x` to the expression `2 + 3`, and then
refer to `x` multiple times.

```
Prelude> let x = 2 + 3
Prelude> x / 2 + x
7.5
Prelude> x + 2
7
```

Aside from the interpreter context, in general Haskell code you can
use the `let ... in ...` construct anywhere an expression is
expected:

```haskell
double :: Integer -> Integer
double n =
  let multiplier = 2
  in  multiplier * n
```

## EXERCISE: Basic arithmetic

Use GHCi to perform the following calculations.  Feel free to use
`let` to make it easier to compose your expressions.

Take your height in feet and inches and convert it to inches using
arithmetic in Haskell (there are twelve inches in one foot).

Then convert that height to centimeters. There are 2.54 centimeters
in one inch.

Lastly, ask someone near you for their height in centimeters.  Find
the average of your heights.
