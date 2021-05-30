### Queue Time

There are a class of problems in computer programming that deal with items coming out of a queue. A great example is the self checkout line at a grocery store, where one line of shoppers wait to check out at multiple registers (for this example imagine that everyone can only checkout one item per second). Write a program thats called **`queue_time`** that will calculate the time it takes for the given **`queue`** to get processed by some number of **`processors`**. This function will have two parameters. The first one, called **`queue`**, will contain integers that representing a task with its value being how long it will take to complete. The second one, called processors, will represent the number of processors to work on the queue.

For example:

```python
queue_time([3, 7, 5], 1) # this will return 15 because it will take 15 units of time to complete processing the queue
queue_time([3, 7, 5], 2) # this will return 8, because the first processor will handle the 3 and 5 task which will take 8 units of time
queue_time([10, 7], 3) # this will return 10, because the longest task in 10 units
queue_time([10, 8, 5, 11, 9], 2) # this will return 22
```
#### ***Solution***

```python
def queue_time(queue, processors):
    pros = [0] * processors
    for time_ in queue:
        pros[pros.index(min(pros))] += time_
        print(pros)
    return max(pros)

```

### Binary Search

When lists get incredibly long it becomes incredibly slow to search through the list. Because of this computer scientists have spent years developing techniques to make finding items in a long list quicker. Binary search is a technique used to find a specific item in a list. Learn more about binary search [here](https://en.wikipedia.org/wiki/Binary_search_algorithm)  . Essentially, binary search boils down to this:

1. The list must be sorted
2. Initially use index 0 and the last index as endpoints
3. Calculate the midpoint of the list (if the length is even round down)
4. Check the value at the midpoint
    - If the midpoint value is the item to find, stop and return the index of that item
    - If the midpoint value is larger than the item to find, set the new upper index to the midpoint
    - If the midpoint value is smaller than the item to find, set the new lower index to the midpoint
5. Repeat this process until the value is found

Write a function called **`bin_search`** that takes two parameters: a **`list`** of items (you can assume this **`list`** is already sorted), and the item for which your function will search. This function should return a tuple of two values: the index of the matching item, and the number of midpoint calculations it took to find that item.

Examples

```python 

bin_search([1, 3, 5, 7, 9], 3)              # -> (1, 1)
bin_search([2, 4, 6, 8, 10, 12], 10)        # -> (4, 2)
bin_search([2, 4, 6, 8, 10, 12], 12)        # -> (5, 0)
bin_search([1, 3, 5, 7, 9, 11, 13, 15], 1)  # -> (0, 0)
```
#### ***Solution***
```python
def bin_search(lst, el):
    iters = 0
    low, high = 0, len(lst) - 1
    while True:
        mid = (high + low) // 2
        if el < lst[mid]:
            high = mid
        else:
            low = mid

        if lst[low] == el:
            return low, iters
        elif lst[mid] == el:
            return mid, iters
        elif lst[high] == el:
            return high, iters

        iters += 1
    raise ValueError("Item not found in list given!")
```

Note, the raise **`ValueError()`** is safety measure included in this function just in case you attempt to find an element that is not present; it is not necessary to include in your solution to this challenge as the test cases used by Learn always include the item to find in the input list.

