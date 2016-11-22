---
layout: post
title: "Pandas Cheatsheet"
comments: true
description: "Cheatsheet for Pandas"
keywords: "pandas, python, cheatsheet"
---

---

## Pandas

The Pandas library is built on NumPy and provides easy-to-use data structures and data analysis tools for the Python programming language.
Use the following import convention:
    
    import pandas as pd

## Pandas Data Structures

### Series

A one-dimensional labeled array A capable of holding any data type 
    
    s = pd.Series([3, -5, 7, 4], index=['a', 'b', 'c', 'd'])

### DataFrame

A two-dimensional labeled data structure with columns of potentially different types

    data = {'Country': ['Belgium', 'India', 'Brazil'],
    'Capital': ['Brussels', 'New Delhi', 'Brasília'],
    'Population': [11190846, 1303171035, 207847528]}

    df = pd.DataFrame(data,
    columns=['Country', 'Capital', 'Population'])

## I/O

### Read and Write to CSV
    
    pd.read_csv('file.csv', header=None, nrows=5)
    pd.to_csv('myDataFrame.csv')

### Read and Write to Excel

    pd.read_excel('file.xlsx')
    pd.to_excel('dir/myDataFrame.xlsx', sheet_name='Sheet1')

### Read multiple sheets from the same file

    xlsx = pd.ExcelFile('file.xls')
    df = pd.read_excel(xlsx, 'Sheet1')

### Read and Write to SQL Query or Database Table
    
    from sqlalchemy import create_engine
    engine = create_engine('sqlite:///:memory:')
    pd.read_sql("SELECT * FROM my_table;", engine)
    pd.read_sql_table('my_table', engine)
    pd.read_sql_query("SELECT * FROM my_table;", engine)

read_sql()is a convenience wrapper around read_sql_table() and
read_sql_query()

    pd.to_sql('myDf', engine)

## Asking For Help
    
    help(pd.Series.loc)

## Selection

### Getting

Get one element
    
    >>> s['b'] 
    
    -5

Get subset of a DataFrame

    >>> df[1:] Get subset of a DataFrame
    
    Country Capital Population
    1 India New Delhi 1303171035
    2 Brazil Brasília 207847528

### Selecting, Boolean Indexing & Setting

#### By Position

Select single value by row & column

    >>> df.iloc([0],[0])
    'Belgium'

    >>> df.iat([0],[0])
    'Belgium'

#### By Label

Select single value by row & column labels

    >>> df.loc([0], ['Country']) 
    'Belgium' 
    >>> df.at([0], ['Country']) 
    'Belgium'

#### By Label/Position

Select single row of subset of rows
    
    >>> df.ix[2]
    Country Brazil 
    Capital Brasília 
    Population 207847528

Select a single column of subset of columns

    >>> df.ix[:,'Capital']
    0 Brussels 
    1 New Delhi
    2 Brasília 
    
Select rows and columns

    >>> df.ix[1,'Capital'] 
    'New Delhi' 

#### Boolean Indexing

Series s where value is not >1
    
    >>> s[~(s > 1)] 

s where value is <-1 or >2
    
    >>> s[(s < -1) | (s > 2)] 

Use filter to adjust DataFrame
    
    >>> df[df['Population']>1200000000] 

#### Setting

Set index a of Series s to 6
    
    >>> s['a'] = 6 

## Dropping

Drop values from rows (axis=0)
    
    >>> s.drop(['a', 'c']) 

Drop values from columns(axis=1)

    >>> df.drop('Country', axis=1) 

## Sort & Rank

Sort by row or column index

    >>> df.sort_index(by='Country') 

Sort a series by its values

    >>> s.order() 

Assign ranks to entries

    >>> df.rank() 

## Retrieving Series/DataFrame Information

### Basic Information

(rows,columns)

    >>> df.shape 

Describe index

    >>> df.index 

Describe DataFrame columns

    >>> df.columns

Info on DataFrame 

    >>> df.info() 

Number of non-NA values

    >>> df.count() 

## Summary

Sum of values

    >>> df.sum() 

Cummulative sum of values

    >>> df.cumsum() 

Minimum/maximum values

    >>> df.min()/df.max() 

Minimum/Maximum index value

    >>> df.idmin()/df.idmax() 

Summary statistics

    >>> df.describe() 

Mean of values

    >>> df.mean() 

Median of values

    >>> df.median() 

## Applying Functions

    >>> f = lambda x: x*2

Apply function

    >>> df.apply(f) 

Apply function element-wise

    >>> df.applymap(f) 

## Data Alignment

### Internal Data Alignment

NA values are introduced in the indices that don’t overlap:
    
    >>> s3 = pd.Series([7, -2, 3], index=['a', 'c', 'd'])
    >>> s + s3
     a 10.0
     b NaN
     c 5.0
     d 7.0

### Arithmetic Operations with Fill Methods

You can also do the internal data alignment yourself with the help of the fill methods:
    
    >>> s.add(s3, fill_value=0)
     a 10.0
     b -5.0
     c 5.0
     d 7.0
    >>> s.sub(s3, fill_value=2)
    >>> s.div(s3, fill_value=4)
    >>> s.mul(s3, fill_value=3)

## Pandas cheat sheet - Summary

I hope this Pandas cheat sheet has been helpful. The Source for this cheat sheet is available [here](https://assets.datacamp.com/blog_assets/PandasPythonForDataScience.pdf).
