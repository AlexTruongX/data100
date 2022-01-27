# Data 100 - Principles and Techniques of Data Science

    University of California, Berkeley
    ds100.org

## Table of Contents
- [Data 100 - Principles and Techniques of Data Science](#data-100---principles-and-techniques-of-data-science)
  - [Table of Contents](#table-of-contents)
  - [Lecture 1 - Course Overview](#lecture-1---course-overview)
    - [What is Data Science?](#what-is-data-science)
    - [Primary Goal in this course](#primary-goal-in-this-course)
    - [Topics covered:](#topics-covered)
    - [The Data Science Life Cycle:](#the-data-science-life-cycle)
  - [Lecture 2 - Sampling and Probability](#lecture-2---sampling-and-probability)
    - [Censuses and Surveys](#censuses-and-surveys)
    - [Sampling: Definitions](#sampling-definitions)
      - [Population, sample, and sampling frame](#population-sample-and-sampling-frame)
      - [Polling Case #1: The Literary Digest](#polling-case-1-the-literary-digest)
      - [Polling Case #2: Gallup's Poll - Election Prediction](#polling-case-2-gallups-poll---election-prediction)
      - [**Common Biases**](#common-biases)
    - [Quality, not quantity!](#quality-not-quantity)
  - [Samples](#samples)
    - [Common Non-Random Samples](#common-non-random-samples)
    - [Probability Sample (aka Random Sample)](#probability-sample-aka-random-sample)
      - [Example Scheme 1: Probability Sample](#example-scheme-1-probability-sample)
    - [Common random sampling schemes](#common-random-sampling-schemes)
      - [Example Scheme 2: Simple Random Sample?](#example-scheme-2-simple-random-sample)
    - [A very common approximation for sampling](#a-very-common-approximation-for-sampling)
    - [Recap of Probability Sampling:](#recap-of-probability-sampling)
  - [Multinomial and Binomial probabilites](#multinomial-and-binomial-probabilites)
    - [Binomial probability: two categories](#binomial-probability-two-categories)
    - [Multinomial probability: multiple categories](#multinomial-probability-multiple-categories)
      - [Generalization of multinomial probabilities](#generalization-of-multinomial-probabilities)
  - [Lecture 3 - Pandas, Part I](#lecture-3---pandas-part-i)
    - [DataFrames](#dataframes)
      - [The DataFrame API](#the-dataframe-api)
      - [> Very Basic Indexing Example](#-very-basic-indexing-example)
    - [Operators](#operators)
      - [[]](#)
    - [Pandas Data Structures](#pandas-data-structures)
      - [Getting a DataFrame Rather than a Series](#getting-a-dataframe-rather-than-a-series)
      - [Retrieving Row and Column Labels](#retrieving-row-and-column-labels)
    - [Conditional Selection](#conditional-selection)
      - [Boolean Array Input](#boolean-array-input)
      - [Alternatives to Boolean Array Selection](#alternatives-to-boolean-array-selection)
    - [Handy Utility Functions](#handy-utility-functions)
      - [Numpy and Built-in Function Support](#numpy-and-built-in-function-support)
        - [`size/shape`](#sizeshape)
        - [`describe`](#describe)
        - [`sample`](#sample)
        - [`value_counts`](#value_counts)
        - [`unique`](#unique)
      - [`sort_values`](#sort_values)



## Lecture 1 - Course Overview

### What is Data Science?
**Data Science** is the application of data centric, computational, and inferential thinking to:

### Primary Goal in this course
Be able to take data and produce useful insights on the world's most challenging and ambiguous problems.

### Topics covered:
![Topics Covered in data 100](../images/IMG_0978.png)

### The Data Science Life Cycle:
![img](../images/IMG_4107.png)
1. Question/Problem Formulation:
   * What do we want to know?
   * What problems are we trying to solve?
   * What are the hypotheses we want to test?
   * What are our metrics for success? 

2. Data Acquisition and Cleaning
   * What data do we have and what data do we need?
   * How will we sample more data?
   * Is our data representative of the population we want to study?

3. Exploratory Data Analysis & Visualizations
   * How is our data organized and what does it contain?
   * Do we already have relevant data?
   * What are the biases, anomalies, or other issues with the data?
   * How do we transform the data to enable effective analysis?

4. Prediction and Inference
   * What does the data say about the world?
   * Does it answer our questions or accurately solve the problem?
   * How robust are our conclusions and can we trust the predictions?


## Lecture 2 - Sampling and Probability
How do we collect data?

### Censuses and Surveys
The US Decennial Census
* was held in April 2020
* counts **every person** living in all 50 states, DC, and US territories (not just citizens)
* Mandated by the Constitution. Participation required by law.
* Important uses:
  * ...


> A **census** is an "official count or survey of a **population**, typically recording various details of individuals.


A **survey** is a set of questions.
* For instance: workers survey individuals and households

What is asked, and how it is asked, can affect:
* How the respondent answers
* *whether* the respondent answers


### Sampling: Definitions
Sampling from a finite population

> Inference: quantifying degree of certainty in our models of the world. 
> 
A **sample** is a subset of the population.
* Samples are used to make *inferences about the population*
* How you draw the sample will affect your accuracy.
* Two common sources of error:
  * **chance error**: random samples can vary from what is expected, in any direction (taking a random sample, and then another and you get different results)
      > Example: Chance error is when your sample is not representative due to random chance, e.g. I survey 10 berkeley students and they are all female just by random happenstance. Bias is because my sampling frame doesn't represent my population, e.g. I do a survey at a sorority to represent the berkeley population.
  * **bias**: a systematic error in one direction
      > Example: If we poll DS100 students who are at lecture, that's an example of bias, as it includes only people who are comfortable being in lecture during Omicron life.

#### Population, sample, and sampling frame
**Population**: The group that you want to learn something aobut
**Sampling Frame**: The list from which the sample is drawn.
* If you're sampling people, the sampling frame is the set of all people that could possibly end up in your sample.
* In what situation would we have a sampling frame that is different than the population?
   > For example, if we took a poll of the people in lecture right now, the sample frame would be whoever showed up to lecture in person. But that isn't representative of the rest of DS100 who may be watching online, watching the webcast, or will never watch it at all.

**Sample**: Who you actually end up sampling.
* A subset of your sampling frame

There may be individuals in your sampling frame (and hence, your sample) that are not in your population! 

![graphic of pop, sample, sample frame difference](../images/IMG_1856.png)

#### Polling Case #1: The Literary Digest
1) The Literary Digest sample was **not representative** of the population.
   * The Digest's **sampling frame:** people in the phonebook, subscribed to magazines, and wnet to country clubs
   * People tended to be richer and vote Republican (Landon).
2) Only 2.4 million people actually filled out the survey!
   * 24% response rate (low)


#### Polling Case #2: Gallup's Poll - Election Prediction
George Gallup, a rising statistician, predicted the election much closer with a sample size of only 50,000!  

He also predicted what The Literary Digest was going to predict within 1%. 

#### **Common Biases**
**Selection Bias**
* Systematically excluding (or favoring) particular groups
* How to avoid: examine the sampling frame and the method of sampling

**Response Bias**
* People don't always respond truthfully.
* How to avoid: examine the nature of questions and the method of surveying.

**Non-response Bias**
* People don't always respond.
* How to avoid: keep your surveys short, and be persistent
* People who don't respond aren't like the people who do!

### Quality, not quantity!
Try to ensure that the sample is representative of the population.
* Don't just try to get a big sample.
* If your method of sampling is bad, and your sample is bag, you will have a **big bad sample!**


## Samples
### Common Non-Random Samples
A **convenience sample** is whoever you can get ahold of.
* Not good idea for inference!
* Haphazard != random
* Sources of bias can can be introduced from things you may not realize

A **quota sample** is a where you first specify your desired breakdown of various subgroups and then reach those targets however you can.
* Reaching quotas "however you can" is not random.
* Your sample will look like your population with respect to a few aspects-but not all.
  * Quotas for age will represent.
  * What about gender, ethnicity? income? 


> Example: You want to sample individuals in your town, and you want the age distribution of your sample to match that of your town's census results.

### Probability Sample (aka Random Sample)
Why sample at random?
1) Random samples **can** produce biased estimates of population characteristics.
   * For example, if we're estimating the maximum of a population.

2) With random samples we are able to estimate the **bias and chance error**.
   * We can quantify the uncertainity


A **probability sample** drawn from random sampling scheme has the following properties:
* You *must* be able to provide the chance that any specified *set* of individuals will be in the sample.
* All individuals in the population *need not* have the same chance of being selected
* You will still be able to measure the errors, because you know al the probabilities. 


#### Example Scheme 1: Probability Sample
...

### Common random sampling schemes
A **random sample with replacement** is a sample drawn *uniformly* (equally likely) at random *with* replacement. 
* Random doesn't ALWAYS mean "uniformly at random," but in this specific context, it does. 

> You could be put back in the raffle box. 

A **simple random sample (SRS)** is a sample drawn uniformly at random *without* replacement.
* Every individual (and subset of individuals) has the same chance of being selected.
* Every pair has the same chance as every other pair.
* Every triple has the same chance as every other triple.
* And so on. 

> If you chose 10 people, you should have the same chance at picking another 10 people. 

#### Example Scheme 2: Simple Random Sample?

1. Is this a probability sample?
   * Yes, that first 10 is 1/10 chance probability. 

2. Does each student have the sample probability of being selected?
   * Yes. Each student is chosen with probability 1/10. You could be in the "line" of whichever n picked between 1 < n < 10. Aka [3, 3+10, 3+20, ...]


3. Is this a simple random sample?
   * No. The chance of selecting (8, 18) is 1/10; the chance of selecting (8,9) is 0.



### A very common approximation for sampling
A common situation in data science:
* We have an enormous population
* We can only afford to sample a relatively small number of individuals.

If the **population is huge** compared to the sample, then random sampling with and without replacement are pretty much the same.

> Example: Suppose there are 10,000 people in a population. Exactly 7,500 of them like Snack 1; the other 2,500 like Snack 2. 
> * SRS (random sample w/o replacement) = .003151
> * Random Sample with Replacement = (0.75)^20 ~= .003171

Pro: Probabilities of sampling with replacement are much easier to compute. 

### Recap of Probability Sampling:
If a sample was **randomly sampled with replacement** from the population:
* It is a probability sample. 
* We can quantify error and bias (to be covered)
* **Given the population distribution**, we can compute the probability of us getting a **particular sample**.



## Multinomial and Binomial probabilites

* `np.random.multinomial` returns these counts

### Binomial probability: two categories
Suppose we have samples at random with replacement 7 times from a bag of marbles:

60% blue marbles, 40% NOT blue marbles

1. What is P(bnbbbnn)?
0.6 * 0.4 * 0.6 * 0.6 * 0.6 * 0.4 * 0.4 = (0.6)⁴(0.4)³

2. P(4 blue, 3 not blue) > P(bnbbbnn):
* Drawn in a specific order = more restrictive and specific than the count 4 blue, 3 not blue. 

P(4 blue, 3 not blue) is the total chance of all those ways and thus:

### Multinomial probability: multiple categories
Look at extra slides 

#### Generalization of multinomial probabilities
Look at extra slides

## Lecture 3 - Pandas, Part I
Introduction to Pandas syntax, operators, and functions

Code (HTML): https://ds100.org/sp22/resources/assets/lectures/lec03/03-pandas-basics.html

Code: https://data100.datahub.berkeley.edu/user/altruong/lab/tree/sp22/lec/lec03/03-pandas-basics.ipynb 

### DataFrames
DataFrame: A (statistical) population from which we draw samples. Each sample has certain features

#### The DataFrame API
The API for the `DataFrame` class is huge. 
* API: "Application Programming Interface"
* The API is the set of abstractions (methods, etc) supported by the class

#### > Very Basic Indexing Example
Most basic task for manipulating a DataFrame: extract rows and columns that we want. 

Most generic: `elections.loc[0:4]` - gives you rows 0 to 4 (inclusive).
* This is not a function since we are splicing.

`loc` also lets us specify the columns that we want as a second argument. 
> `elections.loc[0:4, "Year:" "Party"]`

### Operators
**Loc**

Fundamentally `loc` selects item by **label**
* The labels are the bolded text to the top and left of our dataframe.

*Arguments to loc can be:*
* A list.
  * `elections.loc[[87,25,179], ["Year", "Candidate", "Result]]`
* A slice (syntax is exclusive of the right hand side of the slice).
  * `elections.iloc[[1,2,3], 0:2]`
* A single value.
  * `elections.iloc[[1,2,3], 1]`
* If oyu want all rows, but only some columns you can use : for the left argument
  * `elections.loc[:, ["Year", "Candidate", "Result"]]`


**iloc**

Selects by numbers
Slicing is exclusive (like python, exclude right item)
* A list
  * `elections.iloc[[1,2,3], [0,1,2]]`
  * Give me row 1,2,3 and columns 0,1,2
* Slicing
  * `elections.iloc[[1,2,3], 0:3]`
  * Gives you rows 1,2,3 and columns 0 to 3 (exclusive)
* A single vlaue
  * `elections.iloc[[1,2,3], 1]`
  * Just give me the first column for rows 1,2,3

**Why use loc vs iloc?**

When choosing between `loc` and `iloc`, you'll usually choose `loc`.
* Safer: if the order of columns gets shufled in a public database, your code sitll works.
* Legible: easier to understand what `elections.loc[:, ["Year", "Candidate", "Result]]` means than `elections.iloc[:, [0,1,4]]`

*iloc* can still be useful
* Example: if you have a DataFrame of movie earnings sorted by earnings, can use `iloc` to get the median earnings for a given year (index into the middle).

#### []
* Selection operators
* loc selects items by label. First arugment is rows, second argument is columns
* iloc selects items b y number. First arugment is rows, second argument is columns
* [] only takes on argument which may be:
  * A slice of row numbers
  * A list of column labels
  * A single column label

[] is context sensitive. 

**Examples**
* A slice of 

### Pandas Data Structures
* **Data Frame**: 2D data tabular data
* **Series**: 1D data e.g columnar data
* **Index**: A sequence of row labels (own DS, an array)


Column labels are generally unique

#### Getting a DataFrame Rather than a Series
Two approaches:
* Use `Series.to_frame()`
* Provide a list containing the single column of interest.
  * Looks like double b races


#### Retrieving Row and Column Labels
For row labels, use `DataFrame.index`

For column labels, use `DataFrame.columns`

> How do you turn these into an array? Google it.


### Conditional Selection

#### Boolean Array Input
* Most common way to get specific arrays.
* Needs to be same length as the thing you're indexing.
* Useful because boolean arrays can be generated by using logical operators on Series.

``` python
elections[elections["Party"] == "Independent"]
```

Another example: 
Boolean series can be combined using various operators, allowing filtering of results by multiple criteria
```python
elections[(elections["Result"] == "win") & (elections["%"] < 47)] 
```

#### Alternatives to Boolean Array Selection
* `.isin`
```python
a_parties = ["Anti-Masonic", "American", "Anti-Monopoly", "American Independent"]
elections[elections["Party"].isin(a_parties)]
```
* `str.startswith`
```python
elections[elections["Party"].str.startswith("A")]
```

* `.query`
``` python
# Hug uses this most in his work, very much like SQL
elections[elections["Party"].str.startswith("A")]

# More rich syntax:
parties = ["Republican", "Democratic"]
elections.query('Result == "win" and Party not in @parties')
```

* `.groupby.filter` (lecture 4)
``` python

```

### Handy Utility Functions

#### Numpy and Built-in Function Support

```python
winners = elections.query('Result == "win"')["%"] # Returns series object!

np.mean(winners) # 51.711492943
max(winners) # 61.34470329
```

##### `size/shape`
```python
elections.size # > 1092

elections.shape # (182, 6) -> (row, column) tuple
```

##### `describe`
```python
# gives you a bunch of statistics e.g count, mean, std, min, max, etc
elections.describe()
```

##### `sample`
* If you want a DataFrame consisting of a random selection of rows, you can use the smaple method (SRS):
  * By default, **it is without replacement**. Use `replace=True` for *replacement*
  * Can be chained with other methods and operators (query, iloc, etc)

```python
elections.sample(5).iloc[:, 0:2]

# Example of what code will look like in this class (super nice):
elections.query('Year == 2000').sample(4, replace = True).iloc[:, 0:2]
```

##### `value_counts`
* The `Series.value_counts` method counts the number of occurences of each unique value in a Series
  * Return value is also a Series

```python
elections["Candidate"].value_counts()
```

##### `unique`
The `Series.unique` method returns an array of every unique value in a Series
```python
elections["Party"].unique() # returns numpy array
```

#### `sort_values`
The `DataFrame.sort_values` and `Series.sort_values` methods sort a `DataFrame` (or `Series`).
* The `DataFrame` version requires an argument specifying the column on which to sort

```python
elections["Candidate"].sort_values() # ascending -> a,b,c,d,e

elections.sort_values("%", ascending = False) 

```