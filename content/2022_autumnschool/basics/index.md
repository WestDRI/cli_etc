---
title: "R: the basics"
description: Zoom
colordes: "#e86e0a"
slug: 04_r_basics
weight: 4
execute:
  error: true
format: hugo
---

## Help and documentation

For some general documentation on R, you can run:

``` r
help.start()
```

To get help on a function (e.g. `sum`), you can run:

``` r
help(sum)
```

Depending on your settings, this will open a documentation for `sum` in a pager or in your browser.

## R settings

Settings are saved in a `.Rprofile` file. You can edit the file directly in any text editor or from within R.

List all options:

``` r
options()
```

Return the value of a particular option:

``` r
getOption("help_type")
```

    [1] "html"

Set an option:

``` r
options(help_type = "html")
```

## Assignment

R can accept the equal sign (`=`) for assignments, but it is more idiomatic to use the assignment sign (`<-`) whenever you bind a name to a value and to use the equal sign everywhere else.

``` r
a <- 3
```

Once you have bound a name to a value, you can recall the value with that name:

``` r
a  # Note that you do not need to use a print() function in R
```

    [1] 3

You can remove an object from the environment by deleting its name:

``` r
rm(a)
a
```

    Error in eval(expr, envir, enclos): object 'a' not found

The garbage collector will take care of deleting the object itself from memory.

## Data types and structures

| Dimension | Homogeneous   | Heterogeneous |
|-----------|---------------|---------------|
| 1 d       | Atomic vector | List          |
| 2 d       | Matrix        | Data frame    |
| 3 d       | Array         |               |

### Atomic vectors

#### With a single element

``` r
a <- 2
a
```

    [1] 2

``` r
typeof(a)
```

    [1] "double"

``` r
str(a)
```

     num 2

``` r
length(a)
```

    [1] 1

``` r
dim(a)
```

    NULL

The `dim` attribute of a vector doesn't exist (hence the `NULL`). This makes vectors different from one-dimensional arrays which have a `dim` of `1`.

You might have noticed that `2` is a double (double precision floating point number, equivalent of "float" in other languages). In R, this is the default, even if you don't type `2.0`. This prevents the kind of weirdness you can find in, for instance, Python.

In Python:

``` python
>>> 2 == 2.0
True
>>> type(2) == type(2.0)
False
>>> type(2)
<class 'int'>
>>> type(2.0)
<class 'float'>
```

In R:

``` r
> 2 == 2.0
[1] TRUE
> typeof(2) == typeof(2.0)
[1] TRUE
> typeof(2)
[1] "double"
> typeof(2.0)
[1] "double"
```

If you want to define an integer variable, you use:

``` r
b <- 2L
b
```

    [1] 2

``` r
typeof(b)
```

    [1] "integer"

``` r
mode(b)
```

    [1] "numeric"

``` r
str(b)
```

     int 2

There are six vector types:

-   logical
-   integer
-   double
-   character
-   complex
-   raw

#### With multiple elements

``` r
c <- c(2, 4, 1)
c
```

    [1] 2 4 1

``` r
typeof(c)
```

    [1] "double"

``` r
mode(c)
```

    [1] "numeric"

``` r
str(c)
```

     num [1:3] 2 4 1

``` r
d <- c(TRUE, TRUE, NA, FALSE)
d
```

    [1]  TRUE  TRUE    NA FALSE

``` r
typeof(d)
```

    [1] "logical"

``` r
str(d)
```

     logi [1:4] TRUE TRUE NA FALSE

`NA` ("Not Available") is a logical constant of length one. It is an indicator for a missing value.

Vectors are homogeneous, so all elements need to be of the same type.

If you use elements of different types, R will convert some of them to ensure that they become of the same type:

``` r
e <- c("This is a string", 3, "test")
e
```

    [1] "This is a string" "3"                "test"            

``` r
typeof(e)
```

    [1] "character"

``` r
str(e)
```

     chr [1:3] "This is a string" "3" "test"

``` r
f <- c(TRUE, 3, FALSE)
f
```

    [1] 1 3 0

``` r
typeof(f)
```

    [1] "double"

``` r
str(f)
```

     num [1:3] 1 3 0

``` r
g <- c(2L, 3, 4L)
g
```

    [1] 2 3 4

``` r
typeof(g)
```

    [1] "double"

``` r
str(g)
```

     num [1:3] 2 3 4

``` r
h <- c("string", TRUE, 2L, 3.1)
h
```

    [1] "string" "TRUE"   "2"      "3.1"   

``` r
typeof(h)
```

    [1] "character"

``` r
str(h)
```

     chr [1:4] "string" "TRUE" "2" "3.1"

The binary operator `:` is equivalent to the `seq()` function and generates a regular sequence of integers:

``` r
i <- 1:5
i
```

    [1] 1 2 3 4 5

``` r
typeof(i)
```

    [1] "integer"

``` r
str(i)
```

     int [1:5] 1 2 3 4 5

``` r
identical(2:8, seq(2, 8))
```

    [1] TRUE

### Matrices

``` r
j <- matrix(1:12, nrow = 3, ncol = 4)
j
```

         [,1] [,2] [,3] [,4]
    [1,]    1    4    7   10
    [2,]    2    5    8   11
    [3,]    3    6    9   12

``` r
typeof(j)
```

    [1] "integer"

``` r
str(j)
```

     int [1:3, 1:4] 1 2 3 4 5 6 7 8 9 10 ...

``` r
length(j)
```

    [1] 12

``` r
dim(j)
```

    [1] 3 4

The default is `byrow = FALSE`. If you want the matrix to be filled in by row, you need to set this argument to `TRUE`:

``` r
k <- matrix(1:12, nrow = 3, ncol = 4, byrow = TRUE)
k
```

         [,1] [,2] [,3] [,4]
    [1,]    1    2    3    4
    [2,]    5    6    7    8
    [3,]    9   10   11   12

### Arrays

``` r
l <- array(as.double(1:24), c(3, 2, 4))
l
```

    , , 1

         [,1] [,2]
    [1,]    1    4
    [2,]    2    5
    [3,]    3    6

    , , 2

         [,1] [,2]
    [1,]    7   10
    [2,]    8   11
    [3,]    9   12

    , , 3

         [,1] [,2]
    [1,]   13   16
    [2,]   14   17
    [3,]   15   18

    , , 4

         [,1] [,2]
    [1,]   19   22
    [2,]   20   23
    [3,]   21   24

``` r
typeof(l)
```

    [1] "double"

``` r
str(l)
```

     num [1:3, 1:2, 1:4] 1 2 3 4 5 6 7 8 9 10 ...

``` r
length(l)
```

    [1] 24

``` r
dim(l)
```

    [1] 3 2 4

### Lists

``` r
m <- list(2, 3)
m
```

    [[1]]
    [1] 2

    [[2]]
    [1] 3

``` r
typeof(m)
```

    [1] "list"

``` r
str(m)
```

    List of 2
     $ : num 2
     $ : num 3

``` r
length(m)
```

    [1] 2

``` r
dim(m)
```

    NULL

As with atomic vectors, lists do not have a `dim` attribute. Lists are in fact a different type of vectors.

Lists can be heterogeneous:

``` r
n <- list(2L, 3, c(2, 1), FALSE, "string")
n
```

    [[1]]
    [1] 2

    [[2]]
    [1] 3

    [[3]]
    [1] 2 1

    [[4]]
    [1] FALSE

    [[5]]
    [1] "string"

``` r
typeof(n)
```

    [1] "list"

``` r
str(n)
```

    List of 5
     $ : int 2
     $ : num 3
     $ : num [1:2] 2 1
     $ : logi FALSE
     $ : chr "string"

``` r
length(n)
```

    [1] 5

### Data frames

Data frames contain tabular data. Under the hood, a data frame is a list of vectors.

``` r
o <- data.frame(
  country = c("Canada", "USA", "Mexico"),
  var = c(2.9, 3.1, 4.5)
)
o
```

      country var
    1  Canada 2.9
    2     USA 3.1
    3  Mexico 4.5

``` r
typeof(o)
```

    [1] "list"

``` r
str(o)
```

    'data.frame':   3 obs. of  2 variables:
     $ country: chr  "Canada" "USA" "Mexico"
     $ var    : num  2.9 3.1 4.5

``` r
length(o)
```

    [1] 2

``` r
dim(o)
```

    [1] 3 2

## Indexing

Indexing in R starts at `1`.

``` r
a
```

    [1] 2

``` r
a[1]
```

    [1] 2

``` r
a[2]
```

    [1] NA

``` r
c
```

    [1] 2 4 1

``` r
c[2]
```

    [1] 4

``` r
c[2:4]
```

    [1]  4  1 NA

``` r
j
```

         [,1] [,2] [,3] [,4]
    [1,]    1    4    7   10
    [2,]    2    5    8   11
    [3,]    3    6    9   12

``` r
j[2, 3]
```

    [1] 8

``` r
l
```

    , , 1

         [,1] [,2]
    [1,]    1    4
    [2,]    2    5
    [3,]    3    6

    , , 2

         [,1] [,2]
    [1,]    7   10
    [2,]    8   11
    [3,]    9   12

    , , 3

         [,1] [,2]
    [1,]   13   16
    [2,]   14   17
    [3,]   15   18

    , , 4

         [,1] [,2]
    [1,]   19   22
    [2,]   20   23
    [3,]   21   24

``` r
l[2, 1, 3]
```

    [1] 14

``` r
n
```

    [[1]]
    [1] 2

    [[2]]
    [1] 3

    [[3]]
    [1] 2 1

    [[4]]
    [1] FALSE

    [[5]]
    [1] "string"

``` r
n[3]
```

    [[1]]
    [1] 2 1

``` r
typeof(n[3])
```

    [1] "list"

``` r
n[3][1]
```

    [[1]]
    [1] 2 1

``` r
n[[3]]
```

    [1] 2 1

``` r
typeof(n[[3]])
```

    [1] "double"

``` r
n[[3]][1]
```

    [1] 2

``` r
o
```

      country var
    1  Canada 2.9
    2     USA 3.1
    3  Mexico 4.5

``` r
o[1]
```

      country
    1  Canada
    2     USA
    3  Mexico

``` r
typeof(o[1])
```

    [1] "list"

``` r
str(o[1])
```

    'data.frame':   3 obs. of  1 variable:
     $ country: chr  "Canada" "USA" "Mexico"

``` r
o[[1]]
```

    [1] "Canada" "USA"    "Mexico"

``` r
typeof(o[[1]])
```

    [1] "character"

``` r
o$country
```

    [1] "Canada" "USA"    "Mexico"

``` r
typeof(o$country)
```

    [1] "character"

## Copy-on-modify

While some languages (e.g. Python) do not make a copy if you modify a mutable object, R does.

Let's have a look at Python:

``` python
>>> a = [1, 2, 3]
>>> b = a
>>> b
[1, 2, 3]
>>> a[0] = 4
>>> a
[4, 2, 3]
>>> b
[4, 2, 3]
```

Modifying `a` also modifies `b`. If you want to keep `b` unchanged, you need to explicitly make a copy of `a`.

Now, let's see what happens in R:

``` r
> a <- c(1, 2, 3)
> b <- a
> b
[1] 1 2 3
> a[1] <- 4
> a
[1] 4 2 3
> b
[1] 1 2 3
```

Here, the default is to create a new copy in memory when `a` is transformed so that `b` remains unchanged. This is more intuitive, but more memory intensive.

## Function definition

``` r
compare <- function(x, y) {
  x == y
}
```

We can now use our function:

``` r
compare(2, 3)
```

    [1] FALSE

## Control flow

### Conditionals

``` r
test_sign <- function(x) {
  if (x > 0) {
    "x is positif"
  } else if (x < 0) {
    "x is negatif"
  } else {
    "x is equal to zero"
  }
}
```

``` r
test_sign(3)
```

    [1] "x is positif"

``` r
test_sign(-2)
```

    [1] "x is negatif"

``` r
test_sign(0)
```

    [1] "x is equal to zero"

### Loops

``` r
for (i in 1:10) {
  print(i)
}
```

    [1] 1
    [1] 2
    [1] 3
    [1] 4
    [1] 5
    [1] 6
    [1] 7
    [1] 8
    [1] 9
    [1] 10

Notice that here we need to use the `print()` function.
