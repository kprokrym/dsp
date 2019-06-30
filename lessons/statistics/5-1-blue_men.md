[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)



## Problem: For the following exercises, you can start with chap05ex.ipynb.
## In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters µ = 178 cm and σ = 7.7 cm for men, and µ = 163 cm and σ = 7.3 cm for women. In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf.

Start with chap05ex's selected modules and libraries. We're going to need the norm method from scipy.stats for this.

```python
from __future__ import print_function, division
%matplotlib inline
import numpy as np
import scipy.stats
import nsfg
import first
import analytic
import thinkstats2
import thinkplot
```
Let's figure out how this works.
```python
scipy.stats.norm?
```
We're given the mean (mu) and standard deviation (sigma) for men, which scipy.stats.norm uses as 'loc=' and 'scale=', respectively.
As such, let's get the normal distribution CDF of the data we're interested in. This will let us input the heights we're interested in and see what percentile of men are at that height. 
```python
menheight_normcdf = scipy.stats.norm(loc=178, scale = 7.7).cdf
```
Now let's find how many men are 6'1" (185.42 cm). Same thing for men that are 5'10" (177.8)
```python
menheight_normcdf(185.42), menheight_normcdf(177.8)
```
We get ~83.24% at 6'1" and ~48.96% at 5'10".  To find who falls inside this, subtract the two.  
```python
menheight_normcdf(185.42) - menheight_normcdf(177.8)
```
So ~34% of men are the right height to join the Blue Man Group.


