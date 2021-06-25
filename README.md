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

#### Example 1:
    
Find the mean of the dataset $ A $.
    
$ A = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]$
    
**Step 1**: Sum all of the values in the dataset.
    
$ sum(A) = a_1 + a_2 + a_3 + a_4 + a_5 + a_6 + a_7 + a_8 + a_9 + a_10 $

    
</details>
