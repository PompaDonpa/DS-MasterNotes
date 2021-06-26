# Data Science & Python - Code Snippets

* ###  [Tuples](#tuples)
* ###  [Mean](#mean)
* ###  [Median](#median)
* ###  [Mode](#mode)

<br />

  
<a id="tuples"><h2>A note on tuples</h2></a>

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

<hr />


<a id="mean"><h1>Mean</h1></a>

<details><summary>Summary</summary>
<br />
    
The mean in statistics and probability is likely a familiar concept; the mean is commonly referred to as an average. A mean is derived by calculating a sum of all the values in a collection, then dividing that sum by the total number of items. See below for an example:

$$
\frac{1}{n} \sum_{i=1}^n a_i    
$$    

#### Example 1:
    
Find the mean of the dataset $ A $.
    
$ A = [\quad 1,2,3,4,5,6,7,8,9,10 \quad]$
    
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

<br />

<hr />



<a id="median"><h1>Median</h1></a>

<details><summary>Summary</summary>
<br />

Similar to `mean`, the `median` is another measure of central tendency. The median can be considered the "middle" value of some sorted numerical collection. Half of the collection is equal to or lesser than the median, and half of the collection is equal to or greater than the median. In circumstances where a collection has extreme outliers (specifically datasets which contain outliers which are not symmetrical) the median can be a more robust, or superior measure to the mean. More comparisons between the mean and median are made in the next lesson.
    
> Denoting or relating to a value or quantity lying at the midpoint of a frequency distribution of observed values or quantities, such that there is an equal probability of falling above or below it.
    
#### Example 1:
    
Find the median of the numerical dataset $ A $.
<br />
  
$ A = [\quad 1,2,3,4,5,6,7,8,9 \quad]$
    
    -   The median above is the center value in the sorted list, where there are 
        four items in the collection below the median, and four items above the median.    
<br />
  
_Solution_    
 
$ median(A) = 5 $    

<br />    

#### `Median from an odd-length collection`    
    
When a collection has an odd number of items, determining the median is as simple as sorting the data and identifying the center value. In mathematical terms, in a sorted list of length $\mathit N $, the **index** of the median value is $\frac{N+1}{2} $.
<br />
  
#### Example 2:
    
Consider this example with 11 items: Find the median of the dataset $ B $.
    
$ B = [\quad 10,10,12,13,15,16,17,19,20,20,21 \quad]$

<br />
  
**Step 1 :** Find the length of the dataset
    
$ N = length(B) = 11 $

<br />    
  
**Step 2 :**  Find the index of the center value
    
$ \frac{N+1}{2} = \frac{12}{2} = 6 $   

<br />
  
**Step 3 :** Find the value at the index found in step 2
    
-   The median is located at the 6th index of the sorted list, which is 16. 
    Double check by making sure that there are an equal number of items on either side of the median.

<br />
  
**Solution**
  
<br />
  
$ med(B) = \tilde x_B = 16  $ 

<br />
  
### `Median from an even-length collection`
  
When dealing with collections of an even length there is no term that lies directly in the middle of the collection. In other words, the median of an even-length collection is the `average of the two middle-most values`. Simply find the length of the collection, $ N $, and then take the average of the values at the $ \frac{N}{2} $ and $ \frac{N+1}{2} $indices.

#### Example 3:
    
Find the median of  $ B $ where
    
$ C= [\quad 120, 124, 125, 125, 135, 150, 160, 170 \quad]$

<br />
  
**Step 1 :** Determine whether there are an even or odd number of items
    
$ N = length(C) = 8 $

<br />    
  
**Step 2 **: Find the indices of the two middle-most values
    
$ \frac{N}{2} = 4 \\ \frac{N+1}{2} = 5 $   

<br />
  
**Step 3 :** Find the mean of the $ 4th $ and $ 5th $ terms of $ C $
    
$ med(C) = \tilde x_C = \frac{125+135}{2} = 130 $

<br />
  
**Solution**
<br />
  
Here, the `n'th` (4th) term is 125, and the `(n+1)'th` (5th) term is 135. The mean of these two values is `130`, therefore the median of the collection is `130`. Similar to the previous examples, there is an equal number of items above and below the median (in this case, there are **4** items on each side).

<br />

**Notations :**
  
There is no absolute consensus on the notation for median in statistics, but here are some common notations:  
  
<div align="center" > 
    
|||
|:-:|:---:|
|$ med(A) $| Where $A$ is the collection on which to take the median |
|$ \tilde x $| Lower-case x with a tilde over the top of it is often used to denote the median |

 
</div>  
    
</details>

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

