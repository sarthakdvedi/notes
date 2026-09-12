
### 1. map, filter, reduce -

```python
from functools import reduce

numbers = [1,2,3,4]
print(list(map(lambda x: x*2, numbers)))
print(list(filter(lambda x: x%2==0, numbers)))
print(reduce(lambda x,y:x+y, numbers))
```


###  2. What is the difference between append() and extend()?

Both methods add elements to a list:

- append() adds the entire object as a single element.
- extend() adds each element of an iterable individually.
```python
a = [1,2]
a.append([3,4])
print(a) -->  #[1, 2, [3, 4]]

b = [1,2]
b.extend([3,4])
print(b) --> #[1, 2, 3, 4]
```



### 25. What is the difference between remove(), pop(), and del?

All three remove elements from a list but work differently:

- remove() deletes the first matching value.
- pop() removes an element using its index and returns it.
- del deletes an element or an entire list.
```python
num = [10,20,30,40]

num.remove(20)
num.pop() --> #takes index as arg (default is -1, means last index)

del num[0]

print(num) --> #[30]
```


### 27. How is Exceptional handling done in Python?

Exception handling in Python is used to manage runtime errors gracefully without stopping the program abruptly. Python provides three main keywords for handling exceptions:

- [try](https://www.geeksforgeeks.org/python/python-try-except/): A block of code that is monitored for errors.
- [except](https://www.geeksforgeeks.org/python/python-try-except/): Executes when an error occurs in the try block.
- [finally](https://www.geeksforgeeks.org/python/finally-keyword-in-python/): Executes after the try and except blocks, regardless of whether an error occurred. It’s used for cleanup tasks.

```python
try:

except BaseException: --> #most parent exception class

finally:
```

### 30. What is slicing in Python?

[Slicing](https://www.geeksforgeeks.org/python/python-slice-function/) is a technique used to extract a portion of a sequence such as a string, list, tuple or range. It allows to specify a starting index, an ending index and an optional step value.

> ****Syntax:**** __slice(start, stop, step)__

```python
l = [10, 20, 30, 40, 50]
res = slice(1, 4)
print(l[res])  --> #[20, 30, 40]
```


### 26. What is List Comprehension?
```python
a = [2,3,4,5]
res = [val ** 2 for val in a]
print(res)
```

### 32. What is Dictionary Comprehension?
```python
keys = ['a', 'b', 'c', 'd', 'e']
values = [1, 2, 3, 4, 5]
d = {k: v for k, v in zip(keys, values)}
print(d)
```

### 33. Is Tuple Comprehension possible in Python? If yes, how and if not why?

[Tuple comprehensions](https://www.geeksforgeeks.org/python/why-no-python-tuple-comprehension/) are not directly supported, Python's existing features like generator expressions and the tuple() function provide flexible alternatives for creating tuples from iterable data.

> (i for i in (1, 2, 3))

****Explanation:****

- In Python, expressions enclosed in parentheses with a for loop produce a generator expression, which generates values lazily one at a time.
- Since tuples are immutable sequences, Python does not provide a separate tuple comprehension syntax. Instead, the recommended approach is to use a generator expression and convert it into a tuple using tuple().


### 29. What is the purpose of if __name__ == "__main__" in Python?

The if __name__ == "__main__" statement ensures that a block of code runs only when the file is executed directly, not when it is imported as a module.

```python
def greet():
    print("Hello")

if __name__ == "__main__":
    greet()
```


### 31. Differentiate between List and Tuple?

Let’s analyze the [differences between List and Tuple](https://www.geeksforgeeks.org/python/python-difference-between-list-and-tuple/):

****List****

- Lists are Mutable datatype.
- Lists consume more memory
- The list is better for performing operations, such as insertion and deletion.
- The implication of iterations is Time-consuming

****Tuple****

- Tuples are Immutable datatype.
- Tuple consumes less memory as compared to the list
- A Tuple data type is appropriate for accessing the elements
- The implication of iterations is comparatively Faster


### 35. What are Iterators in Python?

[Iterators](https://www.geeksforgeeks.org/python/iterators-in-python/) are used to iterate a group of elements, containers like a list. Iterators work on iterable objects such as lists, tuples and dictionaries. Python iterator implements __iter__() and the next() methods to iterate the stored elements. We generally use loops to iterate over the collections (list, tuple) in Python.

```python
s = "GFG"
it = iter(s)

print(next(it))
print(next(it))
print(next(it))
```

### 36. What are Magic (Dunder) Methods in Python?

Magic methods are special methods whose names begin and end with double underscores. They allow developers to customize the behavior of objects. Common magic methods include:

```text
- __init__()
- __str__()
- __repr__()
- __len__()
```


### 38. Which sorting technique is used by sort() and sorted() functions of python?

Python uses the [Tim Sort](https://www.geeksforgeeks.org/dsa/timsort/) algorithm for sorting. It’s a stable sorting whose worst case is O(N log N). It’s a hybrid sorting algorithm, derived from merge sort and insertion sort, designed to perform well on many kinds of real-world data.

### 39. What is the difference between sort() and sorted()?

****sort()****

- Sorts original list
- Changes existing list

****sorted()****

- Returns a new sorted list
- Does not modify original list


```python
num = [3,1,2]

print(sorted(num))
print(num)

num.sort()
print(num)
```