# Data Science & Python - Code Snippets

*   [Tuples](#tuples)
*   [Mean](#mean)
*   [Median](#median)
*   [Mode](#mode)
<!-- *   [Markdown](#markdown)
*   [Bash Scripter](#bash-scripter)
*   [Python](#python)
    -   [Comprehensions](#comprehensions)
    -   [Functions](#functions)
        -   [Factorial](#factorial)
        -   [Transpose a Matrix](#transpose) -->
  
# <a id="tuples">A note on tuples</a>

Both enumerate and zip produce a data type called a tuple. You can learn more about the tuple type in Intermediate Python. For now, you can think of a tuple as simply a special kind of list.

For the purposes of using enumerate or zip, the important thing to understand is that they both result in a list of tuple objects:

```python
for tup in enumerate([9, 0, 2, 1, 0]):
    print(tup)
    
(0, 9)
(1, 0)
(2, 2)
(3, 1)
(4, 0)
```
```python
for tup in zip("abc", [1, 2, 3]):
    print(tup)
    
('a', 1)
('b', 2)
('c', 3)
```

Notice that the above code does not use unpacking in the declaration of the for loop, unlike the previous examples in this lesson. This is to demonstrate what kind of object the zip and enumerate produce on each iteration of a loop.

Now, you can actually enumerate over a zip object, but take note of the "shape" of the tuple:

```python
lst_a = [1, 3, 5, 7]
lst_b = [2, 4, 6, 8]

for tup in enumerate(zip(lst_a, lst_b)):
    print(tup)

(0, (1, 2))
(1, (3, 4))
(2, (5, 6))
(3, (7, 8))
```

This can be awkward to deal with, so here's an alternative using a zip object in conjunction with a range object:

```python
lst_a = [1, 3, 5, 7]
lst_b = [2, 4, 6, 8]
enum = range(len(lst_a))

for tup in zip(enum, lst_a, lst_b):
    print(tup)
    
(0, 1, 2)
(1, 3, 4)
(2, 5, 6)
(3, 7, 8)
```
<br />

# <a id="mean">Mean</a>

<details><summary>Summary</summary>
<br />
    
The mean in statistics and probability is likely a familiar concept; the mean is commonly referred to as an average. A mean is derived by calculating a sum of all the values in a collection, then dividing that sum by the total number of items. See below for an example:

$$
\frac{1}{n} \sum_{i=1}^n a_i    
$$    

### Example 1:
    
Find the mean of the dataset $ A $.
    
$ A = [\quad 1,2,3,4\ ,5\ ,6\ ,7\ , 8\ , 9\ , 10\quad]$
    
***Step 1 :*** Sum all of the values in the dataset.
    
$ sum(A) = a_1 + a_2 + a_3 + a_4 + a_5 + a_6 + a_7 + a_8 + a_9 + a_{10} $

***Step 2 :*** Find the number of items in the dataset.

$ length(A) = 10 $

***Step 3:*** Apply the division and come to a solution.
    
$$
mean(A) = \frac{sum(A)}{length(A)} = \frac{55}{10} = 5.5    
$$    
    
    
> The calculation being made above, is formally called the arithmetic mean. There are other types of means (geometric, harmonic), but they are not typically employed in statistics or probability, and this course will not include anything about them.
    
    -   There are a number of common notations for the mean 
        of a collection in statistics, here are the most common:
<div align="center" > 
    
|||
|:-:|:---:|
|$ \mu $| The lowercase greek letter mu is the standard notation for a population mean |
|$ \bar x $| Pronounced "x-bar" is the standard notation for a sample mean |
|$ \bar X $| Capitalized x-bar is a common notation for sample mean, where $ X $ is a random variable|
 
</div>
    
<br /> 
    
### Population vs. Sample
    
In the table above, it is shown that the notation for the mean is different dependent on what type of data the mean is representing.
    
The study of statistics consists of the analysis and study of datasets, and there are two types of datasets, populations and samples. 
    
A `population` represents all of the possible data points or observations from a set of data, for example, a rancher who owns 1000 cattle could take the population mean of their weights by measuring the weight of all 1000 cattle, and taking their mean.  

Conversely, a `sample` does not represent every possible observation, for example, the rancher above could make an estimate of the population mean by taking a random sampling of 100 of the cattle, taking weight measurements, and then taking the mean of those 100 observations.
     
    
</details>

<br />

```python
def mean(lst, trim=0):
    lst_ = lst.copy()
    if trim > 0:
        lst_ = sorted(lst_)[trim:-trim]
    return sum(lst_) / len(lst_)
```
