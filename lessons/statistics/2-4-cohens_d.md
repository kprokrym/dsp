[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)
 Instructions: Communicate the problem, how you solved it, and the solution.
>>
### Problem: Using the variable totalwgt_lb, investigate whether first babies are lighter or heavier than others. Compute Cohen’s d to quantify the difference between the groups. How does it compare to the difference in pregnancy length?


First let's import everything we think we'll need.
```python
from __future__ import print_function, division
%matplotlib inline
import numpy as np
import nsfg
import first

```

Let's designate our variables so we read the file, select live births, and create the first baby vs other babies.
```python
preg = nsfg.ReadFemPreg()
live = preg[preg.outcome == 1]
firsts = live[live.birthord == 1]
others = live[live.birthord != 1]
```
Get a tuple showing the first and other baby mean weights
```python
firsts.totalwgt_lb.mean(), others.totalwgt_lb.mean()
```

Use the function for Cohen's D to calculate the value
Cohen's D is the difference between means divided by the 'pool' (total) variance beween the two samples.
```python
def CohenEffectSize(group1, group2):
    """Computes Cohen's effect size for two groups.
    
    group1: Series or DataFrame
    group2: Series or DataFrame
    
    returns: float if the arguments are Series;
             Series if the arguments are DataFrames
    """
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
    return d
```
Use the function
```python
CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)
```
d = -0.088672927072602 for first weight vs other weight

For reference, the Cohen's D for difference in pregnancy length between first and other births was d = 0.029, given to use during the chapter. 
We see that first births have a lighter total weight than other births and, we can see the d for weight is 3 times larger than the d for length. But this means little in context, especially clinically. A d=.2 difference is considered a "small" difference. We have a .08 difference. This, like length, is clinically negligible. 
