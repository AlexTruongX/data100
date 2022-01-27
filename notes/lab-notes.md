# Lab 1
## Commands
* `arr = np.array([1,2,3])` - create an array of 1,2,3
* `arr[3]` - accessing an array
* `arr[start:end]` - return all elements from start (inclusive) to end (exclusive)
* `arr.shape` - length of array (it's .length, # of items inside each)
* `arr.dtype` - type of data held in the array (e.g int64)


**Note**: Arrays, unlike Python lists, cannot store items of different data types. Arrays will convert everything to the same data type.
* `np.array([1,"3"]) = array(['1', '3')]` - all converted to string
* `np.array([5, 8.3]) = array([5,. , 8.3])` - convereted to doubles

Arrays are also useful in performing *vectorized* operations. Given two or more arrays of equal length, arithmetic will perform element-wise computations across the arrays. 

Example:
```python
# Python list addition will concatenate the two lists
[1, 2, 3] + [4, 5, 6]

# NumPy array addition will add them element-wise
np.array([1, 2, 3]) + np.array([4, 5, 6])
```

**Important Note:** Numpy arrays > python lists. Arrays are miles faster especially with array arithmetic. 

### Boolean Indexing
```python
np.random.seed(42)
random_arr = np.random.rand(60)
evaluatio3n = 2 * random_arr**4
t_f_arr = evaluation > 1 # generates boolean arr, true or false if it passes condition
valid_values = random_arr[t_f_arr] # numpy boolean indexing
```