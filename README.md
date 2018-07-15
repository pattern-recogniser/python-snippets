
### 1. Python String formatting using str.format()
Use {} as placeholders like so:
```variable_1 = 'a'
variable_2 = 'b'
print('This is {} and {}'.format(variable_1, variable_2))
```
outputs

`This is a and b`
This can be used irrespective of the data type of the variables.

#### Reference<br/>
https://www.digitalocean.com/community/tutorials/how-to-use-string-formatters-in-python-3

### 2. Getting the max value of a Numpy array in Python
Use np.argmax() to get the index of the value of the item with the largest value in a Numpy array
```a = np.array([1, 2, 2, 18, 19])
print(np.argmax(a))
```
outputs

`4`

### 3. Applying sum, mean, max, min
For a 1-D numpy array, we can use .sum(), .mean(), .max(), .min()
```a = np.array([1, 2, 2, 18, 19])
print(a.sum())
print(a.mean())
print(a.min())
print(a.max())
```
outputs

`42
8.4
1
19`

### 4. Applying universal functions
For python lists, when you do list_name1 + list_name2, it creates a list with items of second list concatenated to the first list. When you run list_name * some_number, it concatenates the same list thrice and returns a new list.
When you use numpy arrays, if a and b are 2 numpy arrays, element-wise operations are done.
```a = np.array([1, 2, 2, 18, 19])
b = np.array([1, 2, 5, 8, 9])
print(a + b)
```
outputs

`[2  4  7 26 28]`
And similarly with the -, *, \** operations. You can also use & (and), | (or), ~ (not) operators. Ensure you are not using these on integer arrays/ lists, or bitwise operations will be done.

#### Reference
https://docs.scipy.org/doc/numpy-1.14.0/reference/ufuncs.html

### 5. Point to note
When making calculations of %es, and you are dividing 2 integers, make sure you type cast at least one of them to float so that you your final answer is a float % with decimal points.

### 6. In place operators and operators that make a copy
This is a very important concept to understand. There are some operators that perform a calulation on a copy of the original variable, whereas others that change the original variable. To illustrate this point, += is an in-place operator, whereas + is not. Example below:
```
a = np.array([1, 2, 3])
b = a
a += 1
print('b = ', b)
```
gives the value of 
```
b = [2 3 4]
```
whereas
```
a = np.array([1, 2, 3])
b = a
a = a + 1
print('b = ', b)
```
outputs
```
b =  [1 2 3]
```
### 6. Pandas Series 
Built on numpy arrays.
#### Creating a pandas series
  ```
  a = pd.Series([1, 2, 3, 4, 5], index = ['a', 'b', 'c', 'd', 'e'])
  ```
  To access the first element, you can use `a[0]` or `a.loc['e']
- Can use pd_series_name.describe() to give summary statistics of the Pandas series
- Numpy functions such as .sum(), mean(), min(), max() are applicable here 
- If a pandas Series is created without an index, default values of index assigned are 0, 1, 2 ... 
- Note: Index does not mean 'position'
- Pandas Series addition is based on the indices of the 2 series. Addition is done only when the indices match
- Use pandas_series_name.dropna() to drop NaNs, and fillna(0) to fill NaNs with 0
- Use pandas_series_name.apply() to apply a custom function to every element in the Series and return a new Series with the result of the applied function
- Can use pandas_series_name.mean(axis=1) to get mean across rows
- `pandas_series_name.iloc[9]` gives the value in the position 9 (position starts from 0) of the dataframe

### Pandas DataFrames
Series is one-dimensional. When we have mulitple series, we have a Pandas DataFrame.
- `pandas_df_name.iloc[9]` gives the row at the 9th position 
- `pandas_df_name.iloc[0, 3]` gives the element at the 0th row and 3rd column
- `pandas_df_name.loc['index_name', 'header_name']`
- To select one column: `pandas_df_name.['header_name']`
- To select multiple columns: `pandas_df_name.[['header1_name', 'header2_name]]`
- `pandas_df_name.values` - returns a 2-D numpy array - Useful if you want mean() of all values, etc
- `pandas_df_name.describe()` gives a summary of each column of the pandas dataframe
- `pandas_df_name.corrcoef()` - use to get the correlation coefficient

#### Axis names in Pandas
- Instead of axis=0, you can use axis='index', which means summarising along the index, or in other words, you get the mean of the column.
And vice verse axis=1 is equivalent to axis='columns', and you get the mean of each row

#### Other useful points
- When adding 2 dataframes, the index name and the column name should match for the numbers to add up. If there is no corresponding index/column combination, `NaN`s are produced
- Dataframes have the functions `pandas_df_name.add(), sub(), div(), mul()`. In these you can specify parameters like axis=0 to perform row-wise/ column-wise additions. Another available useful option is fill_value=0, which fills `NaN` with 0
- Use `pandas_df_name.applymap(function_name)` to get a Pandas dataframe to which function_name has been applied to every element of the original dataframe
- To easily create buckets in dataframes. Say we have a dataframe with exam grades and want to create grades based on these.
`pd.qcut(pandas_df_name, [0, 0.1, 0.2, 0.5, 0.8, 1], labels=['F', 'D', 'C', 'B', 'A'])`
- `pandas_df_name.apply(function_name)` applies function to a column of the dataframe. Can use axis=1 to apply to a row of the dataframe
