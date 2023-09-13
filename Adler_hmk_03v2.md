# Adler_hmk_03

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

**Question 1:** r x ^It stopped working when I tried to do it

2.  Calculate the product of `x` (from the above question) times π.

``` r
Q2 <- x*pi
```

**Question 2:** r Q2

3.  Use the `getwd()` function to show your current working directory.
    Is that a good working directory, and what program do you think set
    it that way?

    ``` r
    getwd()
    ```

        [1] "C:/Users/meagh/OneDrive - University of Tennessee/Grad Courses/Micro 575"

Question 3: Yes this is a good working directory, it is organized
logically. I am not sure what program you are referring too- I set it to
this directory when I saved the template file in this folder.

## Vectors

1.  Use the `c()` function to create a vector of numbers.

``` r
numbers <- c(sample(1 : 10, size = 10, replace = F)) 
print(numbers)
```

     [1]  2 10  6  1  3  8  9  7  4  5

**Question 1:** r numbers I used the sample function to create a list of
10 random numbers between 1 and 10 that do not repeat.

2.  Use the `c()` function to create a vector of characters.

``` r
characters <- c("A", "B", "C","D","E","F")
print(characters)
```

    [1] "A" "B" "C" "D" "E" "F"

**Question 2:** r characters

3.  Use the `:` implicit function to create a vector of integers from 1
    to 10.

``` r
integers <- c(1:10)
print(integers)
```

     [1]  1  2  3  4  5  6  7  8  9 10

**Questions 3:** r integers

4.  Explain *why* the following code returns what it does. Also address
    whether you think this was a good decision on the part of the
    designers of R?

``` r
v1 <- 1:3
v2 <- c(1:4)
v1 + v2
```

    [1] 2 4 6 5

Question 4: This code is generating a vector “V1” that contains integers
from 1 to 3 and it is being added to another vector “V2” that contains 1
through 4. It is adding them based on index (i.e first entry + first
entry = 2) until the shortest vector is run through then it starts over
from the first entry again. THis is why the last entry is 5 because 1+4
=5

5.  Explain what the following code does. It may be helpful to reference
    the answer to the previous question:

``` r
c(1, 5, 9) + 3
```

    [1]  4  8 12

Question 5: The above code is adding the integer 3 to each of the
entries in the concatenated vector individually and outputing the new,
unsaved vector.

6.  Remove (delete) every variable in your workspace.

``` r
rm(list=ls())
```

Poof!

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

glimpse(penguins)

suppressWarnings()
```

    Rows: 344
    Columns: 8
    $ species           <fct> Adelie, Adelie, Adelie, Adelie, Adelie, Adelie, Adel…
    $ island            <fct> Torgersen, Torgersen, Torgersen, Torgersen, Torgerse…
    $ bill_length_mm    <dbl> 39.1, 39.5, 40.3, NA, 36.7, 39.3, 38.9, 39.2, 34.1, …
    $ bill_depth_mm     <dbl> 18.7, 17.4, 18.0, NA, 19.3, 20.6, 17.8, 19.6, 18.1, …
    $ flipper_length_mm <int> 181, 186, 195, NA, 193, 190, 181, 195, 193, 190, 186…
    $ body_mass_g       <int> 3750, 3800, 3250, NA, 3450, 3650, 3625, 4675, 3475, …
    $ sex               <fct> male, female, female, NA, female, male, female, male…
    $ year              <int> 2007, 2007, 2007, 2007, 2007, 2007, 2007, 2007, 2007…

``` r
ggplot(data=penguins, 
       mapping = aes(x = flipper_length_mm, y = body_mass_g, color = bill_depth_mm)) + geom_point() + geom_smooth(method ="loess")
```

    `geom_smooth()` using formula = 'y ~ x'

    Warning: Removed 2 rows containing non-finite values (`stat_smooth()`).

    Warning: The following aesthetics were dropped during statistical transformation: colour
    ℹ This can happen when ggplot fails to infer the correct grouping structure in
      the data.
    ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
      variable into a factor?

    Warning: Removed 2 rows containing missing values (`geom_point()`).

![Question 2 Penguins](C:\Users\meagh\OneDrive - University of Tennessee\Grad Courses\Micro 575\Adler_hmk_03_files\figure-commonmark\penguin plot HMK3.png)

Question- How do I go to a new line without messing up the function? I
know the indentation is important but when I tried to do it, it was
acting up.

Question - How do I determine what the default size of the points is? I
was trying to change it but size= 1.5 and size = 3 looked the same, and
were too large.

3.  Explain why each aesthetic is mapped at the level that it is (i.e.,
    at the global level, in the `ggplot()` function call, or at the geom
    level, in the `geom_XXX()` function call). Note: A lot of different
    options will work, but some options are clearly better than others.

Question 3: Aesthetic is on the global level within the ggplot function
because no matter how I analyze the data, the data I want to work with
is not changing. In comparsion, I mapped the method of smoothing in the
geom level because if I want to compare different methods or other such
analyzes, I do not want my underlying data visualization to change
because then I can not easily compare the results. An example would be
with the method lm vs loess.
