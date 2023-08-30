# Adler_hmk_02

## Quarto

## Homework 2:  

1.  What were the main issues in the Reinhard and Rogoff issue, and how
    best could they have been avoided?

In the Economist article the key issue was that while they were able to
repeatedly get results within a reasonable ballpark, the ballpark was
wrong. They were missing several data points, from a different variable
combination (high debt, high growth) that resulted in a different trend
in the overall dataset due to a coding error. The error was due to not
selecting an entire row in Excel. This type of error can be avoided in
the future by using coding languages to explicitly select all data
points and avoid manual selection of data. It also likely would have
been caught if someone else tried to replicate the data analysis,
because it’s unlikely they would have missed data/missed the same
datapoints. I am also astounded that the reviewers did not catch this
error, especially since 25% of the data was missing from the
calculations.

2.  What key attributes make a piece of data analysis “reproducible”?
    Please put those attributes in a prioritized list (i.e., for you,
    what is most important, next  most important, etc...)

- The same raw data set is analyzed using the same computational method
  (such as HKY, Bayesian, etc) but not necessarily the same algorithm to
  apply the method, is analyzed by a different person and gets a similar
  result.

- A different raw data set of the same experimental conditions is
  analyzed using the same computational method and algorithm and gets a
  similar result

- A combination of the different raw data sets, analyzed with the same
  method but different algorithms, by a different person to get similar
  results. 

I picked this order because if the original data set can’t be analyzed
by two different people and get the same result then the issue is within
the initial analysis, not the data set. If the data set range is the
issue then that will be revealed in the second reproduction of the
analysis. Such as in the Reinhard and Rogoff issue- since the data was
included in the initial set, the Excel error would probably not be
repeated. And, if the high debt/high growth data points were not
included in the initial dataset then in the second step of comparing two
different raw datasets, it’s more likely another researcher would have
included it. My last step of comparing all the different variables is to
determine if it’s a trend or noise in the data. 

3.  Imagine that you are doing a piece of data analysis that only you
    will ever see: perhaps you are shopping for a car and trying to
    determine what will give you the best value for your money. Should
    you think about making your data analysis reproducible? Why or why
    not?

Yes I would want the data to be reproducible in that if I am designing
code to give me the best value, I need that to apply to any dataset. For
the given example of buying a car, the availability of cars on the
market is going to be constantly changing so the single data point of
the car with the best value will be changing but that doesn’t matter if
the data analyzed is still giving me the best value of the updated
dataset. This is generally applicable to research because as more data
is collected we need to be able to add it into our data analysis as this
will help limit biases and add evidence to support scientific claims.
