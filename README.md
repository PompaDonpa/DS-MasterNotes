
# Challenges

*   [Que Time](#que)
*   [Binary Search](#binary)
*   [Sort by Row or Column](#sort)
*   [Bubble Sort](#bubble)
*   [Caesar Chiper](#caesar)
*   [Valid Parentheses](#parentheses)
*   [Gnome Sort](#gnome)
*   [Magic Methods](#magic)

<br />
<!--     -   [Design Considerations](#design-c)
    -   [Monoliths and Microservices](#monoliths-micro)
        -   [Example](#factorial)
        -   [Nested](#transpose) -->


<a id="que"><h2>Queue Time</h2></a>

There are a class of problems in computer programming that deal with items coming out of a queue. A great example is the self checkout line at a grocery store, where one line of shoppers wait to check out at multiple registers (for this example imagine that everyone can only checkout one item per second). Write a program thats called **`queue_time`** that will calculate the time it takes for the given **`queue`** to get processed by some number of **`processors`**. This function will have two parameters. The first one, called **`queue`**, will contain integers that representing a task with its value being how long it will take to complete. The second one, called processors, will represent the number of processors to work on the queue.

For example:

```python
queue_time([3, 7, 5], 1) # this will return 15 because it will take 15 units of time to complete processing the queue
queue_time([3, 7, 5], 2) # this will return 8, because the first processor will handle the 3 and 5 task which will take 8 units of time
queue_time([10, 7], 3) # this will return 10, because the longest task in 10 units
queue_time([10, 8, 5, 11, 9], 2) # this will return 22
```
#### _Solution_

```python
def queue_time(queue, processors):
    pros = [0] * processors
    for time_ in queue:
        pros[pros.index(min(pros))] += time_
        print(pros)
    return max(pros)

```

<br />

<a id="binary"><h2>Binary Search</h2></a>

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
#### _Solution_
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

<br />


<a id="sort"><h2>Sort by Row or Column</h2></a>

Write a function called sort_by_direction that takes two parameters. The first parameter called seq will be a list of lists where the number of lists is equal to the number of items in each list. The second parameter called direc will give the direction to sort each list of lists. direc will have four possible values, "L" which will sort each row in ascending order, "R" which will sort each row in descending order, "U" which sorts each column in ascending order, and "D" which sorts each column in descending order.

Note that a list of lists can be represented as rows and columns like so:

```python 
[[2, 1, 5],
 [9, 2, 8],
 [1, 7, 3]]
```
#### _Solution_

-    ##### [video](https://www.youtube.com/watch?v=-WWOFR74PuM)

```python
def sort_by_direction(arr, direc):
    if direc == "L" or direc == "R":
        rtn = [sorted(itm, reverse = ("R" == direc)) for itm in arr]
    else:
        lst2sort = []
        for i in range(len(arr)):
            temp = []
            for j in range(len(arr)):
                temp.append(arr[j][i])
            lst2sort.append(temp)

        update = [sorted(itm, reverse = "U" == direc) for itm in lst2sort]
        rtn = []

        for i in range(len(arr)):
            temp = []
            for j in range(len(arr)):
                temp.append(update[j][i])
            rtn.append(temp)
    return rtn
```

<br />

<a id="bubble"><h2>Bubble Sort</h2></a>&emsp;[i](https://en.wikipedia.org/wiki/Bubble_sort)

Bubble sort  is a classic algorithm taught in computer science (and a common interview question). Write a function called **`on_the_bubble`** that takes a **`list`** of numbers as an argument. This function should return a **`tuple`** where the first item represents the number of swaps that were performed in order to sort the **`list`**, and where the second element represents the sorted **`list`** itself.

#### _Solution_

-    [video](https://www.youtube.com/watch?v=Xj_DXB4-jLU)
```python 
def on_the_bubble(lst):
  swaps = 0
  result = lst.copy()

  for _ in range(len(lst)):
    for idx in range(len(lst) - 1 ):
      a, b = result[idx], result[idx + 1]
      if a > b:
        result[idx], result[idx + 1] = b, a
        swaps += 1

  return swaps, result
        
```

<br />

<a id="caesar"><h2>Caesar Chiper</h2></a>

A Caesar Cipher is a classic encryption technique used to encrypt strings. It works by shifting some each letter some amount in the alphabet. For instance, if the shift amount is 2 and the letter is "a" the result will be "c". It also rotates around so if the shift is 2 and the letter is "y" the result will be "a". Learn more about Caesar Ciphers [here](https://en.wikipedia.org/wiki/Caesar_cipher)  . Complete the **`caesar_cipher`** function below. This function takes in two parameters `msg` and **`shift`**, which are the string to be encoded and the size of the shift respectively. This function should return the encrypted string. Note that there wont be any spaces or numbers in the string.

#### _Solution_

```python 
def caesar_cipher(msg, shift):
  alpha = list("abcdefghijklmnopqrstuvwxyz")
  msg_lower = list(msg.lower())
  cypher = []

  for char in msg_lower:
    for idx in range(len(alpha)):
      if char == alpha[idx]:
        if (idx + shift) >= (len(alpha)):
          new_idx = idx + shift - len(alpha)
        else:
          new_idx = idx + shift
        cypher.append(alpha[new_idx])
  return "".join(cypher)

```
```python 
def caesar_cipher(msg, shift):
    alpha = "abcdefghijklmnopqrstuvwxyz" # getting alphabet
    new_msg = "" # new string
    for ltr in msg:
        idx = alpha.index(ltr) + shift # getting the index in alphabet
        if idx > 25:
            idx -= 26 # shifting index
        new_msg += alpha[idx] # adding shifted character
    return new_msg
```

<br />

<a id="parentheses"><h2>Valid Parentheses</h2></a>

Write a function called **`valid_parentheses`** which checks to make sure every **`"("`** has a matching **`")"`**. This function should take in a string, and return a boolean. If every **`"("`** has a matching **`")"`** this function should return **`True`**, if it does not, the function should return **`False`**.

**Example**

```python 
print( valid_parentheses("hi(hi)()") ) # True
print( valid_parentheses("hi())(")   ) # False
print( valid_parentheses(")(test")   ) # False
print( valid_parentheses("()")       ) # True
print( valid_parentheses(")(((()))") ) # False
```

#### _Solution_

```python
def valid_parentheses(string):
    match = 0
    for itm in string:
        if match < 0:
            return False
        if itm == "(":
            match += 1
        elif itm == ")":
            match -= 1
    return match == 0
```

<br />

<a id="gnome"><h2>Gnome Sort</h2></a>

Gnome sort is a technique that expands upon the ideas of bubble sort (see last weeks weekly challenge for bubble sort). Instead of iterating through the whole list and swapping items as they come. Gnome sort finds an item that is out of place and iterates back through the list and places it where it needs to be and then continues going forward through the list. Read more about Gnome sort [here](https://en.wikipedia.org/wiki/Gnome_sort) .

Write a **`gnome_sort`** function that takes in a list and returns a tuple, where the first item is the number times it looped and the second item is the sorted list.

#### _Solution_

```python 
def gnome_sort(lst):
  pos = 0
  count = 0
  result = lst.copy()

  while pos < len(lst):
    a, b = result[pos], result[pos -1]
    if pos == 0 or a >= b:
      pos += 1
    else:
      result[pos], result[pos - 1] = b, a
      pos -= 1
    count += 1
  
  return count, result
```

<br />

<a id="magic"><h2>Magic Methods</h2></a>

<details><summary>Summary</summary>
<br />
    
Magic methods in Python are the special methods which add "magic" to a class. Magic methods are not meant to be invoked directly by a user, but the invocation happens internally from the class on a certain action.
    
**Example:**
    
When two numbers are added together using the + operator, internally, the `__add__()` method will be invoked to complete the addition, and return the sum.
    
    
Magic methods allow user-written classes to participate in Python's built-in functionality. For example, during object creation, Python looks for the magic method called `__init__()`; if `__init__()` exists, Python invokes the method to initialize the object. Likewise, when computing the length of an object using the len() function, Python looks for the magic method called `__len__()`; if `__len__()` exists, Python executes the method to determine the object's length.

So, just as the list and dictionary types provide an implementation of the **__len__()** magic method to allow us to call len() on them, a `__len__()` method can be defined in any class. Once this is done, Python will know what to do when it is passed an instance of a class to the len() function. The implementation of a `__len__()` method is entirely up to the user.
    
    
### Defining a Magic Method

Defining a magic method is the same as defining any other method in a class. In fact, by defining an `__init__()` method for a class in previous lessons, this should be somewhat familiar territory. Again, like any other function or method, start with def, provide the name of the magic method (surrounded by double underscores), list the required parameters in parentheses (don't forget self), and end the line with a colon. In _Code Snippet_, see an example implementation of `__len__()` method in the GalvanizeCourse class that has been used throughout the materials.
    
    
_Code Snippet_
    
```python
# Define the class
class GalvanizeCourse():
    # Define all magic methods
    def __init__(self, name, location, size=0):
        self.name = name
        self.location = location
        self.size = size
        self.questions_asked = []
        if self.size >= 20:
            self.at_capacity = True
        else:
            self.at_capacity = False

    def __len__(self):
        return len(self.questions_asked)

    # Define all other methods
    def add_question_asked(self, question):
        self.questions_asked.append(question)

    def add_students(self, num):
        self.size += num

        if self.size >= 20:
            print('Capacity Reached!!')
            self.at_capacity = True
        else:
            self.at_capacity = False

    def check_if_at_capacity(self):
        return self.at_capacity

# Instantiate object
our_course = GalvanizeCourse('Intro Python', 'Platte', 15)

# Check num of q's asked
print(f'Check #1: {len(our_course)}')

# Add two q's
our_course.add_question_asked("What's he going to show?")
our_course.add_question_asked('Do you know the answer?')

# Check num of q's asked
print(f'Check #2: {len(our_course)}')
    
    
```

```python

Output:
    
Check #1: 0
Check #2: 2  
```
    
Notice that the **len()** function can now interact with instances of `GalvanizeCourse`. As a bit of a motivating question, think about how a real-world implementation of this might look. Perhaps, in a more robust version of this class, there would be a roster attribute which contain a list of `Student` instances, where `Student` is another class in its own right, with attributes and methods. Then perhaps `__len__()` would return the number of student instances in the roster.

Just as one might expect, **len()** now gives the number of questions asked in the course. For reference, in the [notebook](https://colab.research.google.com/drive/1DIgJXznKVNPPBaJsFLZUMSy76bj6XAO4?usp=sharing)  with code examples, try commenting out the definition of `__len__()` and observe the results.
    
    
### Other Magic Methods

<details><summary>Summary</summary>
<br />
    
It turns out that there is a large assortment of magic methods that can be implemented in user-created classes. For example, take a look at what happens when using the `print()` function on the `GalvanizeCourse` class:
    
`<__main__.GalvanizeCourse instance at 0x10a157a28>`

This isn't very informative, this states that the `__main__()` method for a `GalvanizeCourse` instance is at `0x10a157a28`, which is a memory location; while this is very useful to the Python interpretter, there's not much value or human interpretation who wanted some representation of the object displayed on the console. To get a more informative representation of the object, use the `__str__()` method. This is the magic method that Python calls when any object is cast to a string with the `str()` constructor. And, perhaps not surprisingly, Python casts objects to strings whenever the `print()` function is invoked, this is because Python only knows how to output strings to the console.

See an implementation of the `__str__()` method below, after this implementation **print()** can be used to display an instance of `GalvanizeCourse` which is an easily interpretted representation of the object in the console.   
    
_Code Snippet_
    
```python
# Define class
class GalvanizeCourse():
    # Define all magic methods
    def __init__(self, name, location, size=0):
        self.name = name
        self.location = location
        self.size = size
        self.questions_asked = []

        if self.size >= 20:
            self.at_capacity = True
        else:
            self.at_capacity = False

    def __len__(self):
        return len(self.questions_asked)

    def __str__(self):
        our_course_string = '{}, location: {}'
        return our_course_string.format(self.name, self.location)

    # Define all regular methods
    def add_question_asked(self, question):
        self.questions_asked.append(question)

    def add_students(self, num):
        self.size += num

        if self.size >= 20:
            print('Capacity Reached!!')
            self.at_capacity = True
        else:
            self.at_capacity = False

# Create an instance
our_course = GalvanizeCourse('Intro Python', 'Platte', 15)

# Test the print() statement
print(our_course)    
    
```
```python
Output:
    
Intro Python, location: Platte
```
    
Shown above when the `__str__()` method is defined, the `__str__()` method returns an informative string. Now, when an instance of `GalvanizeCourse` is printed, there is something useful.
    

</details>

    
### Another magic method
    
<details><summary>Summary</summary>
<br />
   
If two integers, floats, strings, etc. can be tested for equality with use of the equality operator, `==` , why couldn't a user-created class do the same? As it turns out, this can be done by defining the `__eq__()` method.

    
How does a class know when it's being compared to another object to check for equality? If you take a look at the documentation for the magic `__eq__()` method [here](https://docs.python.org/3.6/reference/datamodel.html#object.__eq__), it shows what the parameters are: `object.__eq__(self, other)`. We already know that **self** is a reference to the object that a method is called on, and **other** is a reference to an object as well, the second parameter in this case.
    
The way that Python evaluates an expression like `x == y` is that it calls the `__eq__()` magic method on the object on the left side the expression (i.e., `x`). As with any other method call, Python passes a reference to the object as the method's first argument **(self)**. Then, it looks on the right side of the `==` and passes a reference to the object there as the second argument to `__eq__()`, in this case `y`. So, the **other** argument that is shown above is just a reference to the second object from the right side of the equality operator. A reference to this object works the same as any other, the attributes and methods of the **other** object can be referenced using dot notation.

For example, consider two instances of **GalvanizeCourse** equal if they have the same name and location. See below for an example:
 
_Code Snippet_
    
```python
class GalvanizeCourse():
    # Define the class
    def __init__(self, name, location, size=0):
        self.name = name
        self.location = location
        self.size = size
        self.questions_asked = []

        if self.size >= 20:
            self.at_capacity = True
        else:
            self.at_capacity = False
    # Magic Methods
    def __len__(self):
        return len(self.questions_asked)

    def __str__(self):
        our_course_string = '{}, location: {}'
        return our_course_string.format(self.name, self.location)

    def __eq__(self, other):
        return self.name == other.name and self.location == other.location

    # Regular Methods
    def add_question_asked(self, question):
        self.questions_asked.append(question)

    def add_students(self, num):
        self.size += num

        if self.size >= 20:
            print('Capacity Reached!!')
            self.at_capacity = True
        else:
            self.at_capacity = False
    
```

Notice that we have access to information about the `other` instance through the usual dot notation. Also, since would expect the result of a `==` expression to be `True` or `False`, we've made our `__eq__()` magic method return a boolean value. In general, you should take special care to make sure to return things from your magic methods that make sense within the context!
 
<br />
    
### More magic methods
    
A good deal of the seemingly simple functionality that is possible using Python built-in types can also be implemented via magic methods in our custom classes. Take a look at [this link](https://docs.python.org/3.6/reference/datamodel.html#special-method-names) to get a sense of all the things magic methods can do.
    
  
</details>    
    
</details>

<br />
    
<a id="magic-challenge"><h3>Magic Methods Challenge</h3></a>
    
Fill in the following methods in the class according to their docstrings. Do not change the name of the class.
    
```python

class LinearPolynomial():
    def __init__(self, m, b):
        self.m = m
        self.b = b

        
    def __str__(self):
        """
        Returns a string representation of the LinearPolynomial instance
        referenced by self.

        Returns
        -------
        A string formatted like:

        mx + b

        Where m is self.m and b is self.b
        """
        pass 

    def __add__(self, other):
        """
        This function adds the other instance of LinearPolynomial
        to the instance referenced by self.

        Returns
        -------
        The sum of this instance of LinearPolynomial with another
        instance of LinearPolynomial. This sum will not change either
        of the instances reference by self or other. It returns the
        sum as a new instance of LinearPolynomial, instantiated with
        the newly calculated sum.
        """
        pass   
    
```
_Solution_
    
```python
class LinearPolynomial():
    def __init__(self, m, b):
        self.m = m
        self.b = b
    
    def __str__(self):
        return f"{self.m}x + {self.b}"
    
    def __add__(self, other):
        return LinearPolynomial( self.m + other.m, self.b + other.b )

    
lp1 = LinearPolynomial(10, 7)
print(lp1) # 10x + 7
    
    
lp2 = LinearPolynomial(20, 14)
print(lp2) # 20x + 14
    
    
print(lp1 + lp2) # 30x + 21
    
```
