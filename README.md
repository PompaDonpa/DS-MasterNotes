# Data Science - MasterNotes

*   [Relevant Links](#relevant-links)
*   [Markdown](#markdown)
*   [Bash Scripter](#bash-scripter)
*   [Python](#python)
    -   [Comprehensions](#comprehensions)
    -   [Functions](#functions)
        -   [Factorial](#factorial)
        -   [Transpose a Matrix](#transpose)
*   [Statistics](#statistics)
    -   [Mean](#mean)
    -   [Median](#median)
    -   [Variance](#variance)
    -   [Standard Deviation](#standard-deviation)
    -   [Permutations](#permutations)
    -   [Combinations](#combinations)
    -   [Bernoulli](#bernoulli)
    -   [Binomial PMF](#binomial-pmf)      

# <a id="relevant-links">Relevant Links</a>

* [Visualizing `scipy.stats` distributions](https://stackoverflow.com/questions/37559470/what-do-all-the-distributions-available-in-scipy-stats-look-like)

* [MathJax basic tutorial and quick reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)

<br />

# <a id="markdown">Markdown</a>

## Anchors / Internal reference links

In standard Markdown, place an anchor `<a name="abcd"></a>` where you want to link to and refer to it on the same page by `[link text](#abcd)`

<br />


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
          [1, 7, 5]]
```
|-|-|-|
|-|-|-|
|2|1|5|
|9|2|8|
|1|7|5|


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
|-|-|-|
|-|-|-|
|2|9|1|
|1|2|7|
|5|8|3|

<br />

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
<br />

### <a id="variance">Variance</a>

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

* **`Population Standard Deviation`**:

$$
\sigma = \sqrt{\frac{1}{n} \sum_{i=1}^{n} (x_i - \mu)^2}
$$

* **`Sample Standard Deviation`**:

$$
s = \sqrt{\frac{1}{n-1} \sum_{i=1}^{n} (x_i - \overline x)^2}
$$



```python
def stdev(lst, sample=True):
    return sqrt(variance(lst, sample))
```
<br />

### <a id="permutations">Permutations</a>

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
* 3 parameters
-   $n$ = number of bernoulli trials
-   $p$ = probability of success on any given bernoulli trial
-   $k$ = specific number of successes for which to find the probability
####    `binomial_pmf(n,p,k)`
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

# Machine Learning Workflow

<br />

### Cross Validation

```python
# train/test split
```

### k-fold Cross Validation

### Bootstrap

<br />
<br />

# Sorting Algorithms 

<br />

## Bubble Sort

```python
# hand coded algorithm
```

```python
# library-called bubble sort
```
<br />
<br />


# `mathplotlib.pyplot` visualizations

<br />


# Derivations
* [Derivation of a Perceptron]()


<br />
<br />

# MathJax
* [Plugin](https://chrome.google.com/webstore/detail/mathjax-plugin-for-github/ioemnmodlmafdkllaclgeombjnmnbima) for GitHub 

$$
\sum_{x=1}^{25} a_x
$$

<br />


## Snappy

* A handy screenshot capturer

## Xnipapp
