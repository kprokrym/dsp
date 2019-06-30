[Think Stats Chapter 4 Exercise 2](http://greenteapress.com/thinkstats2/html/thinkstats2005.html#toc41) (a random distribution)

#### For the following exercises, you can start with chap04ex.ipynb.

Data used in this problem: I'm not the firstborn of my family. I had my baby weight be 7 lb 8 oz.

## Problem: How much did you weigh at birth? Using the NSFG data (all live births), compute the distribution of birth weights and use it to find your percentile rank.
## Using the distribution for others, find your percentile rank in the distribution.

Get the modules we'll want, referencing chap04ex
```python
from __future__ import print_function, division
import numpy as np
import nsfg
import first
import thinkstats2
import thinkplot
%matplotlib inline
```
Load the NSFG data
```python
live, firsts, others = first.MakeFrames()
```
I'm not the first born child, so we're using the 'other' data.
We are using thinkstats2's Cdf object constructor on the 'others' subset of baby weights.
Once we have the CDF, we look at my baby weight (7 lbs 8 oz is 7.5)
```python
other_cdf = thinkstats2.Cdf(others.totalwgt_lb, label='other')
other_cdf.PercentileRank(7.5)
```
55.871, so I'm at the ~56th percentile for non-first born baby weights.  I'm close to the median weight!

For all live births, let's find out my percentile rank.
```python
live_cdf = thinkstats2.Cdf(live.totalwgt_lb, label='live')
live_cdf.PercentileRank(7.5)
```
57.756 ~= 58th percentile for the overall live birth data.