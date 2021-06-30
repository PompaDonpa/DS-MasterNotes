<a id="top"><h1>Data Science - MasterNotes</h1></a>

* ##   [Python](#python)
    -   [Comprehensions](#comprehensions)
    -   [Functions](#functions)
        -   [Factorial](#factorial)
        -   [Transpose a Matrix](#transpose)
* ##   [Statistics](#statistics)
    -   [Mean](#mean)
    -   [Median](#median)
    -   [Mode](#mode)
        -   [Central Tendency](#central-tendency)
    -   [Variance](#variance)
    -   [Five-Number Summary](#five-number)
    -   [IQR](#iqr)
    -   [Outliers](#outliers)
    -   [Remove Outliers](#remove-outliers)
    -   [Standard Deviation](#standard-deviation)
* ##    [Probability](#probability)
    -   [Definition of Set](#def-of-set)
    -   [Set Union](#set-union)
    -   [Set Union for more than 2 events](#set-union2)
    -   [Set Intersection](#set-inter)
    -   [Set Difference](#set-diff)
    -   [Set Complement](#set-complement)
    -   [Calculating Probability](#calc-prob)
    -   [Permutations](#permutations)
    -   [Combinations](#combinations)
        -   [Combinations Itertools](#combinations-itertools)
    -   [Bernoulli](#bernoulli)
    -   [Binomial PMF](#binomial-pmf)
        -   [Binomial PMF Dictionary](#binomial-pmf-dict)
        -   [Poisson PMF](#poisson-pmf)
        -   [Poisson PMF Dictionary](#poisson-pmf-dict)
        -   [Geometric PMF](#geometric-pmf)
    -   [Binomial CDF](#binomial-cdf)
        -   [Binomial CDF Dictionary](#binomial-cdf-dict)
        -   [Poisson CDF](#poisson-cdf)
        -   [Poisson CDF Dictionary](#poisson-pcdf-dict)
        -   [Geometric CDF](#geometric-cdf)
    -   [Axioms of Probability](#axioms-of-prob)

<div align="center">

| | | | | | |  | | | | |
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|[Machine Learning Workflow](#machine-learning)| |[Sorting Algorithms](#sorting-algo)| |[Derivations](#derivations)| |[MathJax](#mathjax)||[Bash Scripter](#bash-scripter)||[Relevant Links](#relevant-links)|

</div>

<hr />        

<br />
  

# <a id="python" >Python</a>

## <a id="comprehensions">Comprehensions</a>

```python 
# Comprehension 
[ num for num in range(100) ]

# Comprehension with condition
[  num for num  in range(100)  if num   > 5    ]
[ char for char in expression  if char in "()" ]
```

<br />

## <a id="functions">Functions</a>

-    #### <a id="factorial">***Factorial***</a>
```python
def factorial(n):
    prod = 1
    for num in range(n+1):
        prod *= num
    return prod
```

-    #### <a id="transpose">***Transpose a Matrix***</a>

```python
matrix = [[2, 1, 5], 
          [9, 2, 8], 
          [1, 7, 3]]
```
<br />

| | | |
|:-:|:-:|:-:|
|2|1|5|
|9|2|8|
|1|7|3|
    

```python 
for row in zip(matrix[0], matrix[1], matrix[2]):
    print(row)
    
(2, 9, 1)
(1, 2, 7)
(5, 8, 3)

list(zip(*matrix))
[ (2, 9, 1), (1, 2, 7), (5, 8, 3) ]
```


```python 
[[*tup] for tup in zip(*matrix)] or
[list(tup) for tup in zip(*matrix)]

[ [2, 9, 1], [1, 2, 7], [5, 8, 3] ]

```
<br />

| | | |
|:-:|:-:|:-:|
|2|9|1|
|1|2|7|
|5|8|3|

<br />

<hr />

# <a id="statistics">Statistics</a>

### <a id="mean">Mean</a>

```python
def mean(lst, trim=0):
    lst_ = lst.copy()
    if trim > 0:
        lst_ = sorted(lst_)[trim:-trim]
    return sum(lst_) / len(lst_)
```

### <a id="median">Median</a>

```python
def median(lst):
    lst_sorted = sorted(lst)
    mid = int(len(lst) / 2)
    # odd
    if len(lst) % 2:
        return lst_sorted[mid]
    else:
        return mean([lst_sorted[mid-1], lst_sorted[mid]])
```

### <a id="mode">Mode</a>

```python
def mode(lst):
    dict_counter = {}
    for item in lst:
        if item in dict_counter.keys():
            dict_counter[item] += 1
        else:
            dict_counter[item] = 1
    max_freq = max(list(dict_counter.values()))
    modes = [item for item, freq in dict_counter.items() if freq == max_freq]
    
    if len(modes) == len(lst):
        return None
    else:
        return modes
```
<br />

### <a id="central-tendency">Central Tendency</a>

<details>
    
+   A measure of central tendency is a single value that attempts to describe a set of data by identifying the central position within that set of data. 
+   As such, measures of central tendency are sometimes called measures of central location. 
+   They are also classed as summary statistics.

    
#### [The Median is Resistant to Outliers](#central-tendency)
*   The primary difference between the mean or median is their levels of resistance to outliers. 
*   The mean is not very resistant to outliers, especially when dealing with a dataset that has non-symmetric outliers.


> If a collection has extreme outliers, the mean may describe the distribution "center" inaccurately. A classic example of this is when looking at household incomes. Households with far greater incomes skew the mean to the point where it no longer accurately describes the dataset.
    
_Example_
    
Consider the incomes of the following ten households. By calculating both the mean and median, it is possible to make a determination as to which of these two statistics describes the incomes most accurately.

$$
A = [\quad\$30\,000,\quad\$35\,000,\quad\$41\,000,\quad\$45\,000,\quad\$50\,000,\quad\$57\,000,\quad\$57\,500,\quad\$59\,000,\quad\$60\,000,\quad\$457\,000\quad]
$$
$$
mean = \mu = \$89,000 \qquad median = \tilde x = \$53,500
$$
> <sub>***Solution***</sub>
> <sub>The mean of the household incomes is **$89,150** and the median is **$53,500**. Here the median does a better job of describing a typical household income from the collection. The mean is greatly skewed by a single income that is far greater than the others. The mean implies that a typical household would have over **$89,000** of income, despite there being only one household with an income greater than **$60,000**.</sub>


#### [The Mean is Preferable in Large Datasets with Few Outliers](#central-tendency)
    
*   There are some situations where the mean is considered a preferable measure to median; typically these are situations in which there are a large number of      items in the collection, and there are not any outliers (or the outliers are symmetric). 
*   Also, inferential statistics are largely built upon measurements of the mean, so it is the statistic which is used most often.
    
    
#### [Mode is Preferable When Using Categorical Data](#central-tendency)
    
*   In a collection with categorical data that is (generally) `not ordinal` in nature, the mode is the best measure of center, though the use of the term "center" may be taking a bit of liberty.

*   The mode can also be a useful descriptive statistic when there isn't one single central concentration of values. 
    
> A common example of this would be the weights of household pets. If one were to take a sample of housepet weights, there would likely be a concentration of cats, each weighing between eight and twelve pounds, and a concentration of dogs weighing between twenty and thirty five pounds. The mean or median may tell us that a typical household pet weighs fifteen pounds, but that description doesn't accurately describe the typical weight of either cats or dogs. A distribution such as this is often referred to as bi-modal.    
 
<div align="center">    
    
|Type of Variable|Best Measure of Central Tendency|
|:-:|:-:|
|Nominal|Mode|
|Ordinal|Median|
|Interval/Ratio (not skewed)|Mean|
|Interval/Ratio (skewed)|Median|
    
</div> 
    
`Skewness` refers to a distortion or asymmetry that deviates from the symmetrical bell curve, or normal distribution, in a set of data. If the curve is shifted to the left or to the right, it is said to be `skewed`.   
    
</details>    

<hr />
<br />

### <a id="five-number">Five-Number Summary</a>


<details>    
The five number summary gives a more in-depth description of a numerical collection of values. In addition to identifying a measure of center `median`, it gives us more insight into the way the values are distributed. The five number summary consists of the following values:

_Five Number Summary_
    
The five-number summary is a set of descriptive statistics that provides information about a dataset. It consists of the five most important sample percentiles

-   The `minimum`
-   The lower (first) quartile: $Q_1$
-   The `median`
-   The upper (third) quartile $Q_3$
-   The `maximum`

> The values are often expressed in a tuple, as follows
  
$ (\quad min,\quad Q_1,\quad median,\quad Q_3,\quad max\quad)$  
    
</details>    
<br />

```python
def five_number_summary(lst):
    sorted_list = sorted(lst)
    lower_half = sorted_list[0: int(len(lst) / 2) + (len(lst) % 2)]
    upper_half = sorted_list[int(len(lst) / 2): ]
    
    q1 = median(lower_half)
    q3 = median(upper_half)
    
    return min(lst), q1, median(lst), q3, max(lst)
```
<br />

### <a id="iqr">IQR</a>

```python
def iqr(lst):
    _, q1, _, q3, _ = five_number_summary(lst)
    
    return q3 - q1
```
<br />


### <a id="outliers">Detect Outliers</a>
```python
def detect_outliers(lst, outlier_coef=1.5):
    outliers = []
    _,q1,_,q3, _ = five_number_summary(lst)
    iqr_ =iqr(lst)
    
    for num in lst:
        if num < q1 -iqr_*outlier_coef or num > q3 + outlier_coef*iqr_:
            outliers.append(num)

    return outliers
    
a = [-500,12,32,54,45,87,89,61,31,12549] 

print(detect_outliers(a,1.5)) # [-500, 12549]
```
<br />

### <a id="remove-outliers">Remove Outliers</a>
```python
def remove_outliers(lst, outlier_coef=1.5):
    outliers = detect_outliers(lst, outlier_coef)
    output = lst.copy()
    
    for num in outliers:
        if num in output:
            output.remove(num)
            
    return output

a =  [590, 615, 575, 608, 350, 1285, 408, 540, 555, 679]
print(remove_outliers(a)) # [590, 615, 575, 608, 540, 555, 679]
```
<br />


### <a id="variance">Variance</a>

<details>

*   The purpose of both the variance and standard deviation statistics are to express an easily interpretable measure of spread in a collection.
*   The variance can be interpreted as the average squared deviations of each number from the mean, and it is calculated as such.
*   The reason why we square the deviations is so we can deal with only positive values, If we didn't square the values our variation would end up being zero for every distribution

    
* **`Population Variance`**


$$\sigma^2 = \frac{1}{n} \sum_{i=1}^{n} (x_i - \mu)^2$$


* **`Sample Variance`**

$$
s^2 = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \overline x)^2
$$

*   **`Recall`**

    * $\mu$ : population mean
    * $\overline x$ : sample mean
    
-   You can see the two formulas for variation are very similar, the primary difference being that the population variance is averaged by dividing by $n$
-   In the computation of a sample standard deviation, we use $n-1$. `The Bessel's correction`
-   This correction is made, because it partially corrects the bias in the estimation of a population variance. [Bessel's](https://en.wikipedia.org/wiki/Bessel%27s_correction)
    
    
_Example 1_
    
>   Find the variance of the following population $A$ assume all measurements are in inches:    
$$ 
A = [\quad 73,\quad 65,\quad72,\quad74,\quad69,\quad70,\quad72,\quad73\quad]
$$

**Step 1 :** Find the mean of $A$
    
$$
\mu = \frac{73+65+72+74+69+70+72+73}{8} = 71
$$    
    
**Step 2 :** Find the sum of the squared differences.
    
$$
\sum_{i=0}^8 (x_i - \mu)^2 \quad = \quad (73-71)^2 + (65-71)^2 + \dots + (73-71)^2 \quad = \quad 60
$$

**Step 3 :** Divide the sum above by $n$ (or multiply by \frac{1}{n})
    
$$
o^2 = \frac{60}{8} = 7.5
$$
    
    
>   <sub>**Solution**</sub>
>   <sub>We can see here that our population variance is $7.5 inches^2$. It is important to note here that a variation calculated will always result in terms of the original unit squared. This leaves something to be desired in terms of interpretability; we'll discuss that in the second half of this lesson when dealing with standard deviations.</sub>    

<br />

_Example 2_
    
>   Calculate the variance for the same numerical collection above, this time assuming it is a sample, call the sample dataset $B$. 
    
$$
B = [\quad 73,\quad 65,\quad72,\quad74,\quad69,\quad70,\quad72,\quad73\quad]
$$

**Step 1 :** Find the mean of $B$
    
$$
\bar x = \frac{73+65+72+74+69+70+72+73}{8} = 71
$$    
    
**Step 2 :** Find the sum of the squared differences.
    
$$
\sum_{i=0}^8 (x_i - \mu)^2 \quad = \quad (73-71)^2 + (65-71)^2 + \dots + (73-71)^2 \quad = \quad 60
$$

**Step 3 :** Divide the sum above by $n$ (or multiply by \frac{1}{n})
    
$$
o^2 = \frac{60}{7} = 8.571
$$
    
    
>   <sub>**Solution**</sub>
>   <sub>The variance of the sample dataset  $B$ is $8.751$, larger than the population's variance.</sub>   

**A note about the application of `Bessel's correction`:**
    
>   The difference in the variances between the sample and the population are a byproduct of applying Bessel's correction. In short, when one finds the variance of a population, they are sure to include all possible outliers. In contrast, when sampling from a population there is a chance that very few (or none!) outliers will end up in the sample dataset. Because of this the variance will likely be smaller than the true variance of the population. Because the object is to make inferences about a population from a sample, the application of Bessel's correction makes the variance from a sample more likely to be accurately representative of the population.    

<br />    
</details>

<br />   


* **`Population Variance`**


$$\sigma^2 = \frac{1}{n} \sum_{i=1}^{n} (x_i - \mu)^2$$


* **`Sample Variance`**

$$
s^2 = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \overline x)^2
$$

*   **`Recall`**

    * $\mu$ : population mean
    * $\overline x$ : sample mean
    
```python
def variance(lst, sample=True):
    mean_ = mean(lst)
    total = 0
    for item in lst:
        total += (item - mean_)**2
    return total / (len(lst) - sample)
```
<br />

### <a id="standar-deviation">Standard Deviation</a>


<details>
    
#### **Population and Sample**    
    
-   As we mentioned above, the variance does a good job of describing the spread of a population or sample. 
-   However imagining the average spread in terms of the original units squared can be difficult to interpret. 
-   Because of this, we typically take the square root of our variance, this yields us a standard deviation. 
-   The standard deviation ends up being in the same units as the original data. 

-   A standard deviation can be informally interpreted as: "a typical item from this collection can be expected to have the value of the mean plus or minus the standard deviation." 
-   This is formally defined by the empirical rule, or the 68/95/99 rule; we won't go into great detail about this rule now, but it will be covered later in the statistics block.
    
<br />
  
***Notations :***
    
$\sigma\quad :$&ensp;lowercase sigma is used for the standard deviation of a population
    
$s\quad :$&ensp;lowercase $s$ is typically used to representation the standard deviation of a sample
    
$sd\quad :$&ensp;the combination of lowercase $sd$ is also commonly used for both standard deviations
   
    
<br />
    
</details>

<br />

* **`Population Standard Deviation`**:

$$
\sigma = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (x_i - \mu)^2}
$$

* **`Sample Standard Deviation`**:

$$
s = \sqrt{\frac{1}{n-1} \sum_{i=1}^{n} (x_i - \overline x)^2}
$$



```python
from math import sqrt

def stdev(lst, sample=True):
    return sqrt(variance(lst, sample))
```
<br />
<hr />



# <a id="probability">Probability</a>

### <a id="def-of-set">Definition of Set</a>
* In mathematics, a set is a well-defined collection of objects
* A set is also an object in itself
* Sets must be comprised of unique objects: **NO DUPLICATES**
* If the outcome of a random experiment is unknown, and all of the possible outcomes are predictable in nature, this set of outcomes is known as the **Sample Space**, notated with a capital $S$, or as the “Universal Set”,  denoted $U$, or $\Omega$ (capital omega)
```python
def dedupe_in_order(lst):
    deduped = []

    for element in lst:
        if element not in deduped:
            deduped.append(element)

    return deduped
```

<br />

### <a id="set-union">Set Union</a>
* The union of two sets is a new set that contains all of the elements that are in at least one of the two sets.
* Common Notation for the union of events A and B: 
* A ∪ B

* There is a distinct relationship between the set theory definition of union, and the logical operator OR.

```python
def union(set1, set2):
    set_union = set1.copy()
    for item in set2:
        if item not in set_union:
            set_union.append(item)
    return set_union
```

<br />


### <a id="set-union2">Set Union for more than 2 events</a>
The union can be extrapolated to more than two events

* Common Notation multiple events: 
* A ∪ B ∪ C
* A ∪ B ∪ C ∪ D

    -   NOTE: The order of the union operation does not matter

```python
def union_mult_sets(*mult_sets):
    set_union = []
    for lst in mult_sets:
        for item in lst:
            if item not in set_union:
                set_union.append(item)
    return set_union
```

<br />

### <a id="set-inter">Set Intersection</a>
* The intersection of two sets is a new set that contains all of the elements that are members of both sets which comprise the intersection
* Common Notation for the intersection of events A and B: 
* AB or A ∩ B
* There is a distinct relationship between the set theory definition of intersection, and the logical operator AND.

```python
def intersection(a,b):
    intersected = []
    for item in a:
        if item in b:
            intersected.append(item)
    return intersected
```

```python
def intersection_mult(*mult_sets):
    set_intersect = []
    if len(mult_sets) > 1 and len(mult_sets[0]) > 0:
        for item in mult_sets[0]:
            is_member = True
            for set_ in mult_sets[1:]:
                if item not in set_:
                    is_member = False
                    break
            if is_member:
                set_intersect.append(item)
    return set_intersect
```

<br />

### <a id="set-diff">Set Difference</a>
* Set Difference is anything in one set that isn’t the other.
    *   Syntax:
        A\B, A-B, A.difference(B)

    *   Example:
        A = {1, 2, 3, 4, 5}
        B = {5, 6, 7, 8, 9}
        A - B = {1, 2, 3, 4}
        B - A = {6, 7, 8, 9}
        
```python
def difference(set1, set2):
    set_difference = []
    for item in set1:
        if item not in set2:
            set_difference.append(item)
    return set_difference
```

<br />

### <a id="set-complement">Complement</a>
*   The complement of a set is the set which represents all members of the sample space which are not in the event.
*   Common Notation for the complement of events A and B: 
*   A’ or Ac or A0 or Ā or ¬A or ~A
*   There is a distinct relationship between the complement and the logical operator NOT

```python
def complement(sample_space, set1):
    return difference(sample_space, set1)
```

<hr />

<br />

## <a id="axioms-of-prob"><h1>Axioms of Probability</h1></a>

## Equating Set Algebra Laws with Boolean Logic

* Consider the concept of `True` as being a logical descriptor for a set $A$ containing $n$ elements.
* In this sense, all the above laws will apply to both Sets and Boolean operations

<br />

<div align="center">

|     Set Operator    | Python Boolean Operator |
|:-------------------:|:-----------------------:|
|Union|`or`|
|Intersection|`and`|
|Complement|`not`|

</div>
    
## Commutative
<br />

* A ∪ B = B ∪ A
* AB = BA

Set Logic

```python
set1 = {'a', 'b', 'c'}
set2 = {'c', 'd', 'e'}

print(set1.union(set2) == set2.union(set1)) # --> True
print(set1.intersection(set2) == set2.intersection(set1)) # --> True
```

Boolean Logic

```python
a = True
b = False

print( (a or b) == (b or a) ) # --> True
print( (a and b) == (b and a) ) # --> True
```    
    

<br />

## Associative
<br />

* (A ∪ B) ∪ C = A ∪ (B ∪ C) = A ∪ B ∪ C
* (AB)C = A(BC) = ABC

Set Logic

```python
set1 = {'a', 'b', 'c'}
set2 = {'c', 'd', 'e'}
set3 = {'a', 'e', 'f'}

print((set1.union(set2)).union(set3) == (set3.union(set2)).union(set1)) # --> True
print((set1.intersection(set2)).intersection(set3) == (set3.intersection(set2)).intersection(set1)) # --> True
```

Boolean Logic

```python
a = True
b = False
c = True

print( ((a or b) or c) == (a or (b or c)) ) # --> True
print( ((a and b) and c) == (a and (b and c)) ) # --> True
```
    

<br />


## Distributive
<br />

* A ∪ (BC) = (A ∪ B)(A ∪ C) 
* A(B ∪ C) = (AB) ∪ (AC)


Set Logic

```python
set1 = {'a', 'b', 'c'}
set2 = {'c', 'd', 'e'}
set3 = {'a', 'e', 'f'}

print( (set2.intersection(set3)).union(set1) == (set1.union(set2)).intersection((set1.union(set3))) ) # --> True
print( (set2.union(set3)).intersection(set1) == (set1.intersection(set2)).union((set1.intersection(set3))) ) # --> True
```

Boolean Logic

```python
a = True
b = False
c = True

print( (a or (b and c)) == ((a or b) and (a or c)) ) # --> True
print( (a and (b or c)) == ((a and b) or (a and c)) ) # --> True   
```
    

<br />


## Idempotent Laws

<br />
    
* _when redundant operations achieve the same result_
* A ∪ A = A
* AA = A



Set Logic

```python
set1 = {'a', 'b', 'c'}

print( set1.union(set1) == set1 ) # --> True
print( set1.union(set1) == set1 ) # --> True
```

Boolean Logic

```python
a = True

print( (a or a) == a ) # --> True
print( (a and a) == a ) # --> True
```   

<br />

## Domination Laws

<br />
    
    
* Recall:
    * U = Universal Set, he set which contains all subsets
    * ∅  = Empty Set = { }
* A ∩ U = A
* A ∩ ∅ = ∅    

</details>

<br />


## Absorption Laws

<br />    
    
* A ∪ (AB) = A
* A(A ∪ B) = A

Set Logic

```python
set1 = {'a', 'b', 'c'}
set2 = {'c', 'd', 'e'}

print( set1.intersection(set2).union(set1) == set1 ) # --> True
print( set1.intersection(set1.union(set2)) == set1) # --> True
```

Boolean Logic

```python
a = True
b = False
c = True

print( (a or (a and b)) == a) # --> True
print( (a and (a or b)) == a) # --> True
```
    

<br />

<hr />


### Identity Property

* A ∪ ∅ = A

### Complement Laws for Universal and Empty Set

* ~∅ = U
* ~U = ∅

### Involution Law
* ~( ~A) = A

```python
a = True
print( (not (not a)) == a) # --> True
```

### A helpful, unnamed law
* AB ∪ A~B = A


```python
a = True
b = False

print( ((a and b) or (a and not b)) == a) # --> True

```

### DeMorgan’s Laws
* 1st: ~(A ∪ B) = ~A ~B
* 2nd: ~(AB) = ~A ∪ ~B

These laws are very helpful for logic and circuit reduction. They are commonly explored in interview questions


### ~(A ∪ B) = ~A ~B

```python
a = True
b = False

print( (not (a or b)) == ((not a) and (not b)) ) # --> True
```


### ~(AB) = ~A ∪ ~B

```python
a = True
b = False

print( (not (a and b)) == (not a or not b) ) # --> True
```


<hr />

<br />

# <a id="calc-prob">Calculating Probability</a>

<details>

### **Probability Theory** 
    
Inferential Statistics is the practice of using mathematical analysis to make inferences about a population from a sample. The mathematics which underly inferential statistics are largely based on probability theory.
    
Calculating probability is attempting to figure out the likelihood of a specific event happening, given some number of attempts. The most fundamental and important probability calcululation is defined as:

The probability of some event $A$ occuring is the number of possible outcomes in that event, divided by the total number of possible outcomes in the sample space. That is,
    
$$
\text{Number of Outcomes in } A = |A| = \text{"The Cardinality of } A\text{"}
$$
$$
\text{Number of Outcomes in } S = |S| = \text{"The Cardinality of } S\text{"}
$$
 
$$
P(A) = \frac{|A|}{|S|}
$$    

***Example***
    
>   Given a fair six-sided die, what is the probability of rolling a 5?
    
$ Event\quad A = \text{Rolling a five}$
    
$P(A) = \frac{1}{6} = .166667$
    
>   <sub>Solution</sub>
>   <sub>The total number of possible outcomes is six, in other words the cardinality of the sample space is six. There is only one outcome in which our die will show five pips, so the cardinality of our event $A$ is 1. Hence, our probability is $\frac{1}{6}$.</sub>
    
<div align="center">
    
|Notation|Meaning|
|:------:|:-----:|    
|$P(A)$|Probability of A|
|$P(A^c)$|Probability of A complement|
|$P(AB)$|Probability of A intersect B|
|$P(A \cup B$|Probability of A union B|
|$P(A \mid B)$|probability of A given B|    
  
    
    
</div>
<hr />
    
</details>
<br />



### <a id="permutations">Permutations</a>

<details>
    
-   A `permutation` is one of several possible variations in which a set or number of objects can be ordered or arranged. 

-   A permutation can be thought of as an arrangement of a number of items
-   $nPk$
    -   where $n$ is the number of possible items
    -   $k$ is how many of those items to arrange

Note: ORDER MATTERS    


<details><summary>Discovery by Counting</summary>

$$
nPk = \frac{n!}{(n-k)!}
$$    
    
If we consider $n$ to be the base of a counting system, then we can determine all permutations $k$ by a counting/reduction approach.
    
1.  Count in base $n$ system
    -   ex: $n = 3$
>   $\text{ 000 010 020 100 110 120 200 210 220 001 011 021 101 111 121 201 211 221 002 012 022 102 112 122 202 212 222 }$
    
2.  Reduce counts that have duplicate items
>   $\text{ 000 010 020 100 110 120 200 210 220 001 011 021 101 111 121 201 211 221 002 012 022 102 112 122 202 212 222 }$
    
3.  Consider $k$ items
    -   ex: $k = 3$
>   |012 | 021 | 102 | 120 | 201 | 210| 
>   |----|-----|-----|-----|-----|-----|
    
-   &emsp;
    -   ex: $k = 2$
>   |12 | 21 | 02 | 20 | 01 | 10| 
>   |---|----|----|----|----|----|

-   &emsp;    
    -   ex: $k = 1$
>   |2|1|0|
>   |-|-|-|
    
    
</details>    
<br />

</details>
<br />

$$
nPk = \frac{n!}{(n-k)!}
$$

```python
def permutations(n, k):
    return int(factorial(n) / factorial(n-k))
```

##### Slightly more optimized:

```python
def permutations(n, k):
    perm = 1
    for i in range(n, n-k, -1):
        perm *= i
    return perm
```
<br />

### <a id="combinations">Combinations</a>

$$
nCk = \frac{n!}{((n-k)! k!)}
$$

```python
def combinations(n, k):
    return int(factorial(n) / (factorial(n-k) * factorial(k)))

# Slightly more optimal:
def combinations(n, k):
    perm = 1
    for i in range(n, n-k, -1):
        perm *= i
    return int(perm / factorial(k))
```
<br />


### <a id="combinations-itertools">Combinations from itertools</a>


```python
def combs_from_itertools(lst, k):
    # get a frozen version of the input
    lst_frozen = tuple(lst)
    n = len(lst_frozen)
    combs = []
    if k > n: return
    indices = list(range(k))
    yield tuple(lst_frozen[i] for i in indices)
    while True:
        for i in reversed(range(k)):
            if indices[i] != i + n - k:
                break
        else:
            return
        indices[i] += 1
        for j in range(i+1, k):
            indices[j] = indices[j-1] + 1
        yield tuple(lst_frozen[i] for i in indices)
    
```
<br />

### <a id="bernoulli">Bernoulli</a>

```python
def bernoulli(p_success=0.5):
    draw = random() # gets a val betw 0 and 1

    if draw < p_success:
        return True
    else:
        return False
```
<br />

### <a id="binomial-pmf">Binomial PMF</a>

####    `binomial_pmf(n,p,k)`

* 3 parameters
-   $n$ = number of bernoulli trials
-   $p$ = probability of success on any given bernoulli trial
-   $k$ = specific number of successes for which to find the probability

$$
P(X=k) = {n \choose k} p^k(1-p)^{n-k}
$$


```python
def binomial_pmf(n, k, p=0.5):
    return combinations(n, k) * (p**k) * (1-p)**(n-k)
```


<br />


### <a id="binomial-pmf-dict">Binomial PMF Dictionary</a>

#### `binomial_pmf_dict()`

This should take 4 parameters:
* `n` the number of trials
* `k_low` the low value of $k$ in the dictionary
* `k_high` the high value of $k$ in the dictionary
* `p=0.5` the probability of success of a given bernoulli trial



```python
def binomial_pmf_dict(n, k_low, k_high, p=0.5):
    d = dict()

    for k in range(k_low, k_high+1):
        d[k] = binomial_pmf(n, k, p)

    return d

d = binomial_pmf_dict(8, 0, 8, p=0.25)

for k, v in d.items():
    print(f'{k}: {v}')
```

<br />

### <a id="poisson-pmf">Poisson PMF</a>

### `poisson_pmf()`

* $e = 2.71828$
* Note, both the constant `e` and the `factorial()` function are available from the `math` module.
* `lambda`&ensp;The average number of occurances in a certain time.  

$$
P(\lambda, k \text{ events}) = \frac{e^{-\lambda}\lambda^k}{k!}
$$

```python
from math import e, factorial

# print(e) # 2.718281828459045

def poisson_pmf(lmbda, k):
    return lmbda**k * e**(-lmbda) / factorial(k)
```
<br />

### <a id="poisson-pmf-dict">Poisson PMF Dictionary</a>
### `poisson_pmf_dict()`
* your parameters will be 
    * `lmbda`
    * `low_k`
    * `high_k`

Holding `lmbda` constant, write a function that returns a dictionary showing the probs for number of events from `low_k` to `high_k` (inclusive)

```python
def poisson_pmf_dict(lmbda, low_k, high_k):
    d = dict()

    for k in range(low_k, high_k+1):
        d[k] = poisson_pmf(lmbda, k)

    return d

d = poisson_pmf_dict(10, 0, 30)

for k, v in d.items():
    print(f'{k}: {round(v, 6)}')
```
<br />

### <a id="geometric-pmf">Geometric PMF</a>
### `geometric_pmf()`

* `p` : probability
* `k` : number of failures (inclusive or exclusive of the 1st success)
* `inclusive=True` : whether or not to use inclusive or exclusive pmf

PMF calculating the number of trials up to **and including** the first success

$$
P(X=k) = p (1-p)^{k-1}
$$

PMF calculating the number of trials **before** the first success

$$
P(X=k) = p (1-p)^{k}
$$

```python
def geometric_pmf(p, k, inclusive=True):
    return p * (1-p)**(k-inclusive)
    # if inclusive:
    #     return p * (1-p)**(k-1)
    # else:
    #     return p * (1-p)**k
```
<br />




<br />

### <a id="binomial-cdf">Binomial CDF</a>

####    `binomial_cdf(n, k_high, p=0.5)`

$$
P(X \le k) = \sum_{i=0}^k {n \choose i}p^i(1-p)^{n-i}
$$


```python
def binomial_cdf(n, k_high, p=0.5):
    cumulative = 0.0

    for k in range(0, k_high+1):
        cumulative += binomial_pmf(n, k, p)

    return cumulative
```

<br />


### <a id="binomial-cdf-dict">Binomial CDF Dictionary</a>

#### `binomial_cdf_dict()`


<br />

### <a id="poisson-cdf">Poisson PMF</a>

### `poisson_pmf()`

<br />


### <a id="poisson-cdf">Poisson CDF Dictionary</a>
### `poisson_cdf()`
* your parameters will be 
    * `lmbda`
    * `high_k`

```python
def poisson_cdf(lmbda, k_high):
    cdf = 0.0

    for k in range(k_high+1):
        cdf += poisson_pmf(lmbda, k)

    return cdf
```

<br />

### <a id="geometric-cdf">Geometric CDF</a>
### `geometric_cdf()`




<br />

<hr />

# <a id="machine-learning">Machine Learning Workflow</a>

<br />

### <a id="cross-validation">Cross Validation</a>
### <a id="k-cross">k-fold Cross Validation</a>

<hr />

<br />


# <a id="sorting-algo">Sorting Algorithms</a> 

<br />

## <a id="bubble-sort">Bubble Sort</a>

```python
# hand coded algorithm
# library-called bubble sort
```

<br />
<hr />


# <a id="derivations">Derivations</a>
* [Derivation of a Perceptron](https://levelup.gitconnected.com/training-a-single-perceptron-405026d61f4b)



<br />
<hr />

# <a id="mathjax">MathJax</a>
* [Plugin](https://chrome.google.com/webstore/detail/mathjax-plugin-for-github/ioemnmodlmafdkllaclgeombjnmnbima)
* [MathJax basic tutorial and quick reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
* [LateX Basic Code](http://www.malinc.se/math/latex/basiccodeen.php)
* [Greek Symbols & Letters](https://www.overleaf.com/learn/latex/List_of_Greek_letters_and_math_symbols)
* [Mathematical Symbols](https://oeis.org/wiki/List_of_LaTeX_mathematical_symbols)

<div align="center">

$$\sum_{n=1}^\infty \frac{1}{n^2} \to
  \textstyle \sum_{n=1}^\infty \frac{1}{n^2} \to
  \displaystyle \sum_{n=1}^\infty \frac{1}{n^2}$$
  
$\displaystyle \lim_{t \to 0} \int_t^1 f(t)\, dt$
versus $\lim_{t \to 0} \int_t^1 f(t)\, dt$.

$\Biggl(\biggl(\Bigl(\bigl((\: x \: )\bigr)\Bigr)\biggr)\Biggr)$

</div>

<br />
<hr />


# <a id="bash-scripter">Bash Scripter</a>
* bash profile location on OSX : `~./bash_profile`

```bash
function gitadder(){
git pull
git add .
git commit -m "Auto Updated: $(date '+%a)%M:%H %h %d %Y)"
git push
}
```

<br />
<hr />



# <a id="relevant-links">Relevant Links</a>

* ### `Tools`

* [Kaggle](https://www.kaggle.com/learn)
* [Awesome Python](https://github.com/os/awesome-python)
* [Awesome Machine Learning](https://github.com/josephmisiti/awesome-machine-learning)
* [Presto - Distributed SQL Query Engine for Big Data](https://prestodb.io/) 

<hr />

* ### `Lectures`

* [JB Statistics](https://www.jbstatistics.com/)
* [Introduction to Statistical Learning (ISLR)](https://static1.squarespace.com/static/5ff2adbe3fe4fe33db902812/t/6009dd9fa7bc363aa822d2c7/1611259312432/ISLR+Seventh+Printing.pdf)
* [Elements of Statistical Learning (ESL)](https://web.stanford.edu/~hastie/Papers/ESLII.pdf)
* [Machine Learning with Python - freeCodeCamp](https://www.freecodecamp.org/learn/machine-learning-with-python/)
* [100 Days of Machine Learning](https://github.com/CodesOfRa/100-Days-Of-ML-Code)
* [Learn Machine learning in 3Mo](https://github.com/CodesOfRa/Learn_Machine_Learning_in_3_Months)

<hr />

* ### `Advanced`

* [Neural Network](https://playground.tensorflow.org/#activation=tanh&batchSize=10&dataset=circle&regDataset=reg-plane&learningRate=0.03&regularizationRate=0&noise=0&networkShape=4,2&seed=0.74045&showTestData=false&discretize=false&percTrainData=50&x=true&y=true&xTimesY=false&xSquared=false&ySquared=false&cosX=false&sinX=false&cosY=false&sinY=false&collectStats=false&problem=classification&initZero=false&hideText=false) 
* [Visualizing `scipy.stats` distributions](https://stackoverflow.com/questions/37559470/what-do-all-the-distributions-available-in-scipy-stats-look-like)
* [Tutorial on Deep Learning for Vision](https://sites.google.com/site/deeplearningcvpr2014/)

* [Awesome Public Dataset](https://github.com/awesomedata/awesome-public-datasets)
* [Data Science & Machine Learning in Production](https://github.com/eugeneyan/applied-ml) 

<hr />

* ### `Other`

* [50 Cognitive Biases in the Modern World](https://www.visualcapitalist.com/50-cognitive-biases-in-the-modern-world/)
* [PHD Research by Chandan Singh](https://csinva.io/)




<hr />

### [UP](#top)
