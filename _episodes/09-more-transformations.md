---
title: "More Transformations"
teaching: 5
exercises: 15
questions:
- "How can we iteratively use transformations to clean up data?"
- "What happens when we split data into several columns?"
objectives:
- "Learn how to find new expressions in the documentation"
- "Learn how to combine expressions to save time"
keypoints:
- "There are mulitple expressions that you can use to get the same result"
- "Sometimes adding columns can help with sticky data problems"
---

## Writing more transformations

Reminder:
GREL functions are written by giving a value of some kind (a text string, a date, a number etc.) to a GREL function. Some GREL functions take additional parameters or options which control how the function works. 

GREL supports two types of syntax:

* ```value.function(options)```
* ```function(value, options)```

Either is valid, and which is used is completely down to personal preference. In these notes the first syntax is used.

### Two ways to split data 

Ideally, we would only have one piece and one type of information in a cell in a table. As we know, this isn't always the case with data we get from other sources. There are two different ways we can separate data in a cell in OpenRefine:
* Creating new rows in the same column ```Edit cells > Split multi-valued cells...```
* Creating new columns for each piece of data ```Edit columns > Split into several columns...```

>## When would we want new rows versus new columns? 
>
> If each piece of data is in the same category, you will want to create new rows in the same column. Then those values can be compared against each other like we did in the author example.
>
> If the data are in different categories you will want to create new columns. We are going to work with the *Citation* column, which has several kinds of data in one cell. 
>
> Note: These techniques only work if the data is consistently formatted. If there are inconsistencies then splitting the data will create additional problems. 
{: .challenge}

>## Let's look closer at the *Citation* column and determine what we want it to look like. 
>
> 1. How many different kinds of data are in the column?
> 2. How many different separators are there?
> 3. Are the data all formatted the same? Can we assume if we split the data our columns will have the same category of data for each row?
>
>>## Solution
>>1. There are 5 kinds of data, so we will need at least 5 columns.
>>2. There are 2 obvious separators (*,*, *)*) and 1 that may not have been so obvious (*-*). 
>>3. It looks like it, but it depends on how granular you want to get. There are some discrepancies in how page numbers are represented.
>{: .solution}
{: .challenge}

### Splitting one column into several columns

The citation column can be split into at least 5 columns, but the separators aren't the same for all types of data. This is going to be an iterative process where the order in which we do things is important. The separator to create 4 of the 5 columns is *,*, so we will separate the columns using that first. 

In the *Split into several columns...* you can leave the default values set. 

>## Where might identifying the number of columns be useful?
>
> Take a minute to think about situations where you might want to limit the number of columns.
{: .challenge}

You should have 4 new columns named **Citation 1**, **Citation 2**, **Citation 3**, and **Citation 4**. 

We can now split **Citation 4**, which contains page numbers and the year, into two columns using "(" as the separator. We will have **Citation 4 1** and **Citation 4 2**. We can now rename all of the columns - **Journal name**, **Volume**, **Issue**, **Page numbers**, **Year**. The **Year** column still has the extra **)**, so let's figure out how to get rid of it.

>## Getting rid of unwanted characters
>
> There are several ways to get rid of unwanted characters. Take a look at the [GREL String Functions](https://github.com/OpenRefine/OpenRefine/wiki/GREL-String-Functions) to see how we might accomplish this.  
>
>>## Solution
>>1. Chomp - chomp(value,")")
>>2. Slice - slice(value, 0, 4) **Note: GREL works on base 0 and ranges need to go to the first character you don't want to include.**
>>3. Replace - replace(value, ")", "")
>>4. Replace Characters - replaceChars(value, ")","")
>{: .solution}
{: .challenge}



