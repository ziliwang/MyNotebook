#### 过滤索引
```python
>>> a = pd.DataFrame({'a': [1,2,3,4,5,6], 'b': [6,5,4,3,2,1]})
>>> a
   a  b
0  1  6
1  2  5
2  3  4
3  4  3
4  5  2
5  6  1
>>> a['a'].isin([2,4,6])
0    False
1     True
2    False
3     True
4    False
5     True
Name: a, dtype: bool
>>> a[a['a'].isin([2,4,6])]
   a  b
1  2  5
3  4  3
5  6  1
```
