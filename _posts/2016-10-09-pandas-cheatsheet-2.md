---
layout: post
title: "Pandas Cheatsheet Part 2"
comments: true
description: "Cheatsheet for Pandas"
keywords: "pandas, python, cheatsheet"
---

---

# Pandas and Friends

# What does it do?

Pandas is a Python data analysis tool built on top of NumPy that provides a
suite of data structures and data manipulation functions to work on those data
structures.  It is particularly well suited for working with time series data.

# Getting Started - Installation

Installing with pip or apt-get::

    pip install pandas
    # or
    sudo apt-get install python-pandas

* Mac - Homebrew or MacPorts to get the dependencies, then pip
* Windows - Python(x,y)?
* Commercial Pythons: Anaconda, Canopy

# Getting Started - Dependencies

Dependencies, required, recommended and optional

    # Required
    numpy, python-dateutil, pytx
    # Recommended
    numexpr, bottleneck
    # Optional
    cython, scipy, pytables, matplotlib, statsmodels, openpyxl

# Pandas' Friends!

Pandas works along side and is built on top of several other Python projects.

* IPython

* Numpy

* Matplotlib

## Pandas gets along with EVERYONE!

# Background - IPython


IPython is a fancy python console.  Try running ``ipython`` or ``ipython --pylab`` on your command line.  Some IPython tips

    # Special commands, 'magic functions', begin with %
    %quickref, %who, %run, %reset
    # Shell Commands
    ls, cd, pwd, mkdir
    # Need Help?
    help(), help(obj), obj?, function?
    # Tab completion of variables, attributes and methods

# Background - IPython Notebook

There is a web interface to IPython, known as the IPython notebook, start it
like this

    ipython notebook
    # or to get all of the pylab components
    ipython notebook --pylab

# IPython - Follow Along

Follow along by connecting to TMPNB.ORG!

* [http://tmpnb.org](http://tmpnb.org)

# Background - NumPy

* NumPy is the foundation for Pandas
* Numerical data structures (mostly Arrays)
* Operations on those.
* Less structure than Pandas provides.

# Background - NumPy - Arrays


    import numpy as np
    # np.zeros, np.ones
    data0 = np.zeros((2, 4))

    data0

    array([[ 0.,  0.,  0.,  0.],
           [ 0.,  0.,  0.,  0.]])

    # Make an array with 20 entries 0..19
    data1 = np.arange(20)
    # print the first 8
    data1[0:8]

    array([0, 1, 2, 3, 4, 5, 6, 7])



## Background - NumPy - Arrays


    # make it a 4,5 array
    data = np.arange(20).reshape(4, 5)
    data

    array([[ 0,  1,  2,  3,  4],
           [ 5,  6,  7,  8,  9],
           [10, 11, 12, 13, 14],
           [15, 16, 17, 18, 19]])



## Background - NumPy - Arrays

Arrays have NumPy specific types, `dtypes`, and can be operated on.


    print("dtype: ", data.dtype)
    result = data * 20.5
    print(result)

    ('dtype: ', dtype('int64'))
    [[   0.    20.5   41.    61.5   82. ]
     [ 102.5  123.   143.5  164.   184.5]
     [ 205.   225.5  246.   266.5  287. ]
     [ 307.5  328.   348.5  369.   389.5]]


Now, on to Pandas
-----------------

Pandas
------

* Tabular, Timeseries, Matrix Data - labeled or not
* Sensible handling of missing data and data alignment
* Data selection, slicing and reshaping features
* Robust data import utilities.
* Advanced time series capabilities

Data Structures
----------------

* Series - 1D labeled array
* DataFrame - 2D labeled array
* Panel - 3D labeled array (More D)

# Assumed Imports

In my code samples, assume I import the following


    import pandas as pd
    import numpy as np

# Series

* one-dimensional labeled array
* holds any data type
* axis labels known as index
* implicit integert indexes
* ``dict``-like

# Create a Simple Series


    s1 = pd.Series([1, 2, 3, 4, 5])
    s1

    0    1
    1    2
    2    3
    3    4
    4    5
    dtype: int64



# Series Operations


    # integer multiplication
    print(s1 * 5)

    0     5
    1    10
    2    15
    3    20
    4    25
    dtype: int64


# Series Operations - Cont.


    # float multiplication
    print(s1 * 5.0)

    0     5
    1    10
    2    15
    3    20
    4    25
    dtype: float64


# Series Index


    s2 = pd.Series([1, 2, 3, 4, 5],
                   index=['a', 'b', 'c', 'd', 'e'])
    s2

    a    1
    b    2
    c    3
    d    4
    e    5
    dtype: int64



# Date Convenience Functions

A quick aside ...


    dates = pd.date_range('20130626', periods=5)
    print(dates)
    print()
    print(dates[0])

    <class 'pandas.tseries.index.DatetimeIndex'>
    [2013-06-26, ..., 2013-06-30]
    Length: 5, Freq: D, Timezone: None
    ()
    2013-06-26 00:00:00


# Datestamps as Index


    s3 = pd.Series([1, 2, 3, 4, 5], index=dates)
    print(s3)

    2013-06-26    1
    2013-06-27    2
    2013-06-28    3
    2013-06-29    4
    2013-06-30    5
    Freq: D, dtype: int64


# Selecting By Index

Note that the integer index is retained along with the new date index.

    print(s3[0])
    print(type(s3[0]))
    print()
    print(s3[1:3])
    print(type(s3[1:3]))

    1
    <type 'numpy.int64'>
    ()
    2013-06-27    2
    2013-06-28    3
    Freq: D, dtype: int64
    <class 'pandas.core.series.Series'>


# Selecting by value

    s3[s3 < 3]

    2013-06-26    1
    2013-06-27    2
    Freq: D, dtype: int64

# Selecting by Label (Date)


    s3['20130626':'20130628']

    2013-06-26    1
    2013-06-27    2
    2013-06-28    3
    Freq: D, dtype: int64

Series Wrapup
-------------

Things not covered but you should look into:

* Other instantiation options: ``dict``
* Operator Handling of missing data ``NaN``
* Reforming Data and Indexes
* Boolean Indexing
* Other Series Attributes:

  * ``index`` - ``index.name``
  * ``name`` - Series name

DataFrame
---------

* 2-dimensional labeled data structure
* Like a SQL Table, Spreadsheet or ``dict`` of ``Series`` objects.
* Columns of potentially different types
* Operations, slicing and other behavior just like ``Series``

# DataFrame - Simple


    data1 = pd.DataFrame(np.random.rand(4, 4))
    data1

<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td> 0.002581</td>
      <td> 0.851980</td>
      <td> 0.097265</td>
      <td> 0.648841</td>
    </tr>
    <tr>
      <th>1</th>
      <td> 0.732965</td>
      <td> 0.820690</td>
      <td> 0.895176</td>
      <td> 0.582483</td>
    </tr>
    <tr>
      <th>2</th>
      <td> 0.176504</td>
      <td> 0.068942</td>
      <td> 0.466759</td>
      <td> 0.918777</td>
    </tr>
    <tr>
      <th>3</th>
      <td> 0.938426</td>
      <td> 0.097954</td>
      <td> 0.696534</td>
      <td> 0.684424</td>
    </tr>
  </tbody>
</table>
</div>

# DataFrame - Index/Column Names

    dates = pd.date_range('20130626', periods=4)
    data2 = pd.DataFrame(
        np.random.rand(4, 4),
        index=dates, columns=list('ABCD'))
    data2

<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-06-26</th>
      <td> 0.831222</td>
      <td> 0.209279</td>
      <td> 0.340186</td>
      <td> 0.928447</td>
    </tr>
    <tr>
      <th>2013-06-27</th>
      <td> 0.252513</td>
      <td> 0.452392</td>
      <td> 0.862822</td>
      <td> 0.738837</td>
    </tr>
    <tr>
      <th>2013-06-28</th>
      <td> 0.309083</td>
      <td> 0.822918</td>
      <td> 0.924720</td>
      <td> 0.964607</td>
    </tr>
    <tr>
      <th>2013-06-29</th>
      <td> 0.827998</td>
      <td> 0.539519</td>
      <td> 0.248369</td>
      <td> 0.377682</td>
    </tr>
  </tbody>
</table>
</div>


# DataFrame - Operations


    data2['E'] = data2['B'] + 5 * data2['C']
    data2

<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
      <th>E</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-06-26</th>
      <td> 0.831222</td>
      <td> 0.209279</td>
      <td> 0.340186</td>
      <td> 0.928447</td>
      <td> 1.910210</td>
    </tr>
    <tr>
      <th>2013-06-27</th>
      <td> 0.252513</td>
      <td> 0.452392</td>
      <td> 0.862822</td>
      <td> 0.738837</td>
      <td> 4.766505</td>
    </tr>
    <tr>
      <th>2013-06-28</th>
      <td> 0.309083</td>
      <td> 0.822918</td>
      <td> 0.924720</td>
      <td> 0.964607</td>
      <td> 5.446516</td>
    </tr>
    <tr>
      <th>2013-06-29</th>
      <td> 0.827998</td>
      <td> 0.539519</td>
      <td> 0.248369</td>
      <td> 0.377682</td>
      <td> 1.781366</td>
    </tr>
  </tbody>
</table>
</div>



See?  You never need Excel again!

# DataFrame - Column Access

Deleting a column.


    # Deleting a Column
    del data2['E']
    data2




<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-06-26</th>
      <td> 0.831222</td>
      <td> 0.209279</td>
      <td> 0.340186</td>
      <td> 0.928447</td>
    </tr>
    <tr>
      <th>2013-06-27</th>
      <td> 0.252513</td>
      <td> 0.452392</td>
      <td> 0.862822</td>
      <td> 0.738837</td>
    </tr>
    <tr>
      <th>2013-06-28</th>
      <td> 0.309083</td>
      <td> 0.822918</td>
      <td> 0.924720</td>
      <td> 0.964607</td>
    </tr>
    <tr>
      <th>2013-06-29</th>
      <td> 0.827998</td>
      <td> 0.539519</td>
      <td> 0.248369</td>
      <td> 0.377682</td>
    </tr>
  </tbody>
</table>
</div>



# DataFrame

Remember this, data2, for the next examples.


    data2

<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2013-06-26</th>
      <td> 0.831222</td>
      <td> 0.209279</td>
      <td> 0.340186</td>
      <td> 0.928447</td>
    </tr>
    <tr>
      <th>2013-06-27</th>
      <td> 0.252513</td>
      <td> 0.452392</td>
      <td> 0.862822</td>
      <td> 0.738837</td>
    </tr>
    <tr>
      <th>2013-06-28</th>
      <td> 0.309083</td>
      <td> 0.822918</td>
      <td> 0.924720</td>
      <td> 0.964607</td>
    </tr>
    <tr>
      <th>2013-06-29</th>
      <td> 0.827998</td>
      <td> 0.539519</td>
      <td> 0.248369</td>
      <td> 0.377682</td>
    </tr>
  </tbody>
</table>
</div>



# DataFrame - Column Access 

As a dict

    data2['B']

    2013-06-26    0.209279
    2013-06-27    0.452392
    2013-06-28    0.822918
    2013-06-29    0.539519
    Freq: D, Name: B, dtype: float64

# DataFrame - Column Access

As an attribute

data2.B

    2013-06-26    0.209279
    2013-06-27    0.452392
    2013-06-28    0.822918
    2013-06-29    0.539519
    Freq: D, Name: B, dtype: float64

# DataFrame - Row Access

By row label

    data2.loc['20130627']    

    A    0.252513
    B    0.452392
    C    0.862822
    D    0.738837
    Name: 2013-06-27 00:00:00, dtype: float64

# DataFrame - Row Access

By integer location   

    data2.iloc[1]

    A    0.252513
    B    0.452392
    C    0.862822
    D    0.738837
    Name: 2013-06-27 00:00:00, dtype: float64



# DataFrame - Cell Access

Access column, then row or use iloc and row/column indexes.


    print(data2.B[0])
    print(data2['B'][0])
    print(data2.iloc[0,1])  # [row,column] 

    0.209279059059
    0.209279059059
    0.209279059059


# DataFrame - Taking a Peek

Look at the beginning of the DataFrame


    data3 = pd.DataFrame(np.random.rand(100, 4))
    data3.head()

<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td> 0.796264</td>
      <td> 0.332496</td>
      <td> 0.860904</td>
      <td> 0.488276</td>
    </tr>
    <tr>
      <th>1</th>
      <td> 0.405906</td>
      <td> 0.309003</td>
      <td> 0.159129</td>
      <td> 0.597427</td>
    </tr>
    <tr>
      <th>2</th>
      <td> 0.107366</td>
      <td> 0.791943</td>
      <td> 0.080191</td>
      <td> 0.187125</td>
    </tr>
    <tr>
      <th>3</th>
      <td> 0.176196</td>
      <td> 0.931741</td>
      <td> 0.742967</td>
      <td> 0.953014</td>
    </tr>
    <tr>
      <th>4</th>
      <td> 0.567175</td>
      <td> 0.673101</td>
      <td> 0.069275</td>
      <td> 0.208249</td>
    </tr>
  </tbody>
</table>
</div>



# DataFrame - Taking a Peek

Look at the end of the DataFrame.

    data3.tail()

<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>95</th>
      <td> 0.175699</td>
      <td> 0.187918</td>
      <td> 0.407732</td>
      <td> 0.441582</td>
    </tr>
    <tr>
      <th>96</th>
      <td> 0.638801</td>
      <td> 0.264603</td>
      <td> 0.210135</td>
      <td> 0.721955</td>
    </tr>
    <tr>
      <th>97</th>
      <td> 0.947213</td>
      <td> 0.674040</td>
      <td> 0.087639</td>
      <td> 0.240926</td>
    </tr>
    <tr>
      <th>98</th>
      <td> 0.220907</td>
      <td> 0.309761</td>
      <td> 0.659022</td>
      <td> 0.894547</td>
    </tr>
    <tr>
      <th>99</th>
      <td> 0.452450</td>
      <td> 0.365101</td>
      <td> 0.043229</td>
      <td> 0.911712</td>
    </tr>
  </tbody>
</table>
</div>



# DataFrame Wrap Up

Just remember, 

* A `DataFrame` is just a bunch of `Series` grouped together.
* Any one dimensional slice returns a `Series`
* Any two dimensional slice returns another `DataFrame`.
* Elements are typically NumPy types or Objects.

# Panel

Like DataFrame but 3 or more dimensions.

# IO Tools

Robust IO tools to read in data from a variety of sources

* CSV - [pd.read_csv()](http://pandas.pydata.org/pandas-docs/stable/io.html#io-read-csv-table)
* Clipboard - [pd.read_clipboard()](http://pandas.pydata.org/pandas-docs/stable/io.html#clipboard)
* SQL - [pd.read_sql_table()](http://pandas.pydata.org/pandas-docs/stable/io.html#sql-queries)
* Excel - [pd.read_excel()](http://pandas.pydata.org/pandas-docs/stable/io.html#io-excel)

# Plotting

* Matplotlib - [s.plot()](http://pandas.pydata.org/pandas-docs/stable/visualization.html#plotting-with-matplotlib) - Standard Python Plotting Library
* Trellis - [rplot()](http://pandas.pydata.org/pandas-docs/stable/rplot.html) - An 'R' inspired Matplotlib based plotting tool

# Bringing it Together - Data

The csv file (``phx-temps.csv``) contains Phoenix weather data from
GSOD::

    1973-01-01 00:00:00,53.1,37.9
    1973-01-02 00:00:00,57.9,37.0
    ...
    2012-12-30 00:00:00,64.9,39.0
    2012-12-31 00:00:00,55.9,41.0

# Bringing it Together - Code

Simple `read_csv()`

    # simple readcsv
    phxtemps1 = pd.read_csv('phx-temps.csv')
    phxtemps1.head()

<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>1973-01-01 00:00:00</th>
      <th>53.1</th>
      <th>37.9</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td> 1973-01-02 00:00:00</td>
      <td> 57.9</td>
      <td> 37.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td> 1973-01-03 00:00:00</td>
      <td> 59.0</td>
      <td> 37.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td> 1973-01-04 00:00:00</td>
      <td> 57.9</td>
      <td> 41.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td> 1973-01-05 00:00:00</td>
      <td> 54.0</td>
      <td> 39.9</td>
    </tr>
    <tr>
      <th>4</th>
      <td> 1973-01-06 00:00:00</td>
      <td> 55.9</td>
      <td> 37.9</td>
    </tr>
  </tbody>
</table>
</div>



# Bringing it Together - Code

Advanced `read_csv()`, parsing the dates and using them as the index, and naming the columns.


    # define index, parse dates, name columns
    phxtemps2 = pd.read_csv(
        'phx-temps.csv', index_col=0,
        names=['highs', 'lows'], parse_dates=True)
    phxtemps2.head()

<div style="max-height:1000px;max-width:1500px;overflow:auto;">
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>highs</th>
      <th>lows</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1973-01-01</th>
      <td> 53.1</td>
      <td> 37.9</td>
    </tr>
    <tr>
      <th>1973-01-02</th>
      <td> 57.9</td>
      <td> 37.0</td>
    </tr>
    <tr>
      <th>1973-01-03</th>
      <td> 59.0</td>
      <td> 37.0</td>
    </tr>
    <tr>
      <th>1973-01-04</th>
      <td> 57.9</td>
      <td> 41.0</td>
    </tr>
    <tr>
      <th>1973-01-05</th>
      <td> 54.0</td>
      <td> 39.9</td>
    </tr>
  </tbody>
</table>
</div>



# Bringing it Together - Plot


    import matplotlib.pyplot as plt
    %matplotlib inline 
    phxtemps2.plot()  # pandas convenience method

    <matplotlib.axes._subplots.AxesSubplot at 0x7fca44e8e550>

![png]({{ site.baseurl }}/assets/images/output_pandas_part2_1.png)


Boo, Pandas and Friends would cry if they saw such a plot.

# Bringing it Together - Plot

Lets see a smaller slice of time:


    phxtemps2['20120101':'20121231'].plot()

    <matplotlib.axes._subplots.AxesSubplot at 0x7fca3c66f1d0>

![png]({{ site.baseurl }}/assets/images/output_pandas_part2_2.png)


# Bringing it Together - Plot

Lets operate on the `DataFrame` ... lets take the differnce between the highs and lows.

    phxtemps2['diff'] = phxtemps2.highs - phxtemps2.lows
    phxtemps2['20120101':'20121231'].plot()

    <matplotlib.axes._subplots.AxesSubplot at 0x7fca3c6ba650>




![png]({{ site.baseurl }}/assets/images/output_pandas_part2_3.png)


# Pandas Alternatives

* AstroPy seems to have similar data structures.
* I suspect there are others.

References
----------

* [Pandas Documentation](http://pandas.pydata.org/pandas-docs/stable/index.html)
* [Python for Data Analysis](http://www.amazon.com/Python-Data-Analysis-Wes-McKinney/dp/1449319793/)
* [Presentation Source](https://github.com/desertpy/presentations)


# Thanks! - Pandas and Friends

* Austin Godber
* Mail: godber@uberhip.com
* Twitter: @godber
* Presented at [DesertPy](http://desertpy.com), Jan 2015.
* [Ipython Notebook](https://tmp58.tmpnb.org/user/Ijb0G3wtgqaT/notebooks/communities/desertpy/pandas-intro-godber-jan-2014/Pandas_and_Friends.ipynb#)
