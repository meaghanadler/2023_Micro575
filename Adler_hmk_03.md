# Adler Homework 3

# Base R and R Basics

HINT: Remember that you can get help on any function by typing
`?`(function name). For instance, `?rnorm` gives help on the `rnorm()`
function.

## Creating and naming variables

1.  Create a variable called `x` and use it to store the result of the
    calculation `(3*(4+2)`.

``` r
x <- (3*(4+2))
```

2.  Calculate the product of `x` (from the above question) times π.

``` r
Q2 <- x*pi
```

3.  Use the `getwd()` function to show your current working directory.
    Is that a good working directory, and what program do you think set
    it that way?

    ``` r
    getwd()
    ```

        [1] "C:/Users/meagh/OneDrive - University of Tennessee/Grad Courses/Micro 575"

Yes this is a good working directory, the project is saved with a
logical name. Rstudio is the program setting the project location (not
R).

## Vectors

1.  Use the `c()` function to create a vector of numbers.

``` r
numbers <- c(sample(1 : 10, size = 10, replace = F)) 
print(numbers)
```

     [1]  5  3  7  9  2  4  1  8  6 10

I used the sample function to create a list of 10 random numbers between
1 and 10 that do not repeat.

2.  Use the `c()` function to create a vector of characters.

``` r
characters <- c("A", "B", "C","D","E","F")
print(characters)
```

    [1] "A" "B" "C" "D" "E" "F"

3.  Use the `:` implicit function to create a vector of integers from 1
    to 10.

``` r
integers <- c(1:10)
print(integers)
```

     [1]  1  2  3  4  5  6  7  8  9 10

4.  Explain *why* the following code returns what it does. Also address
    whether you think this was a good decision on the part of the
    designers of R?

``` r
v1 <- 1:3
v2 <- c(1:4)
v1 + v2
```

    [1] 2 4 6 5

Explanation:

This code is generating a vector “V1” that contains integers from 1 to 3
and it is being added to another vector “V2” that contains 1 through 4.
It is adding them based on index (i.e first entry + first entry = 2)
until the shortest vector is run through then it starts over from the
first entry again. THis is why the last entry is 5 because 1+4 =5

5.  Explain what the following code does. It may be helpful to reference
    the answer to the previous question:

``` r
c(1, 5, 9) + 3
```

    [1]  4  8 12

The above code is adding the integer 3 to each of the entries in the
concatenated vector individually and outputing the new, unsaved vector.

6.  Remove (delete) every variable in your workspace.

``` r
rm(list=ls())
```

![poof!](https://i.gifer.com/3klP.gif)

## Graphics

1.  Load the tidyverse package. **NOTE:** Be sure to use the chunk
    option `message=FALSE` to suppress the messages that tidyverse
    prints when loaded. These messages are useful in the

``` r
library(tidyverse)
message =FALSE
```

2.  Recreate the visualization of `body_mass_g` to `flipper_length_mm`,
    from the penguins data set, that is shown in question 8 of section
    2.2.5 of [R4DS](https://r4ds.hadley.nz/data-visualize).

``` r
library(tidyverse)
library(palmerpenguins)

plt=ggplot(data=penguins, 
       mapping = aes(x = flipper_length_mm, y = body_mass_g, color = bill_depth_mm)) + geom_point() + geom_smooth(method ="loess")


suppressWarnings(print(plt))
```

    `geom_smooth()` using formula = 'y ~ x'

![](Adler_hmk_03_files/figure-commonmark/unnamed-chunk-11-1.png)

3.  Explain why each aesthetic is mapped at the level that it is (i.e.,
    at the global level, in the `ggplot()` function call, or at the geom
    level, in the `geom_XXX()` function call). Note: A lot of different
    options will work, but some options are clearly better than others.

Explanation:

Aesthetic is on the global level within the ggplot function because no
matter how I analyze the data, the data I want to work with is not
changing. In comparsion, I mapped the method of smoothing in the geom
level because if I want to compare different methods or other such
analyzes, I do not want my underlying data visualization to change
because then I can not easily compare the results. An example would be
with the method lm vs loess.
