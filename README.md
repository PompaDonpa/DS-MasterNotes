# Data Science - MasterNotes
<br />

*   [Markdown](#markdown)

# Relevant Links

<br />

* [Visualizing `scipy.stats` distributions](https://stackoverflow.com/questions/37559470/what-do-all-the-distributions-available-in-scipy-stats-look-like)

* [MathJax basic tutorial and quick reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)

<br />
------------------------------
# <a name="markdown">Markdown</a>

## Anchors / Internal reference links

In standard Markdown, place an anchor `<a name="abcd"></a>` where you want to link to and refer to it on the same page by `[link text](#abcd)`

<br />
------------------------------

# Bash Scripter
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
------------------------------

# Python

## Comprehensions

```python
[num for num in range(100)]
```

## Functions to remember

```python
def factorial(n):
    prod = 1
    for num in range(n+1):
        prod *= num
    return prod
```

<br />
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
------------------------------

# Derivations
* [Derivation of a Perceptron]()


<br />
<br />

# LaTex
* won't render in GitHub, but will in VSCode

<br />

$$
\sum_{x=1}^{25} a_x
$$

<br />
------------------------------

## Snappy

* A handy screenshot capturer

## Xnipapp
