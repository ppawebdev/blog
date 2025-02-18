---
authors: [ "Geoffrey Hunter" ]
categories: [ "Mathematics", "Statistics" ]
date: 2019-08-02
draft: false
lastmod: 2019-08-02
tags: [ "mathematics", "statistics", "standard deviation" ]
title: "Standard Deviation"
type: "page"
---

{{% warning %}}
This page is a work-in-progress.
{{% /warning %}}

## Overview

The standard deviation is a metric which is used to measure the amount of variation in a set of data values.

The standard deviation has the same units as the data.

## Equation

<div>$$ \sigma = \sqrt{\frac{ \sum{(x - \bar{x})?^2}}{n}} $$</div>

<p class="centered">
where:<br>
\( \bar{x} \) is the mean (average) of the samples<br>
\( n \) is the number of samples<br>
</p>

For example,

```
4, 8, 7, 3, 12
```

<div>
\begin{align}
\bar{x} &= \frac{1}{5} * (4+8+7+3+12)\\
        &= 6.8\\
\\
\sum{(x - \bar{x})} = (4-6.8)^2+(8-6.8)^2+(7-6.8)^2+(3-6.8)^2+(12-6.8)^2\\
                  =                  
\end{align}
</div>

## Software

You can calculated the standard deviation of an array in Numpy with `np.std()`:

```python
np.std(my_array)
```

By default, the array is flattened. However, you can specify an `axis` on which to calculate the standard deviation.