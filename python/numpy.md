#### 矩阵翻转 - flip
```python
>>> a = np.fromfunction(lambda i,j: i+j, (5,2))
>>> a
array([[ 0.,  1.],
       [ 1.,  2.],
       [ 2.,  3.],
       [ 3.,  4.],
       [ 4.,  5.]])
>>> np.flip(a, axis=1)  # 垂直翻转
array([[ 1.,  0.],
       [ 2.,  1.],
       [ 3.,  2.],
       [ 4.,  3.],
       [ 5.,  4.]])
>>> np.flip(a, axis=0)  # 水平翻转
array([[ 4.,  5.],
       [ 3.,  4.],
       [ 2.,  3.],
       [ 1.,  2.],
       [ 0.,  1.]])
```
#### 矩阵函数映射
```python
>>> a = np.fromfunction(lambda i,j: i+j, (2,2))
>>> a
array([[ 0.,  1.],
       [ 1.,  2.]])
>>> mapping_dict = {0: 'zero', 1: 'one', 2: 'two', 3: 'three'}
>>> np.vectorize(lambda i: mapping_dict[i])(a)
array([['zero', 'one'],
       ['one', 'two']],
      dtype='<U4'
```
#### 按值对索引排序
##### argsort
```python
>>> a = np.fromfunction(lambda i,j: i+j, (2,6))
>>> a
array([[ 0.,  1.,  2.,  3.,  4.,  5.],
       [ 1.,  2.,  3.,  4.,  5.,  6.]])
>>> np.argsort(a)[:,::-1][:,:3]  # 前三
array([[5, 4, 3],
       [5, 4, 3]])
```
##### argpartition
```python
>>> a = np.fromfunction(lambda i,j: i+j, (2,6))
>>> a
array([[ 0.,  1.,  2.,  3.,  4.,  5.],
       [ 1.,  2.,  3.,  4.,  5.,  6.]])
>>> np.flip(np.argpartition(a, -3, axis=1), axis=1)[:,:3]
array([[5, 4, 3],
       [5, 4, 3]])
```
##### 对比
```python
>>> d = list(range(1000))
>>> random.shuffle(d)
>>> %timeit np.argsort(d)[-3:]
90.7 µs ± 464 ns per loop (mean ± std. dev. of 7 runs, 10000 loops each)
>>> %timeit np.argpartition(d, -3)[-3:]
62 µs ± 66.6 ns per loop (mean ± std. dev. of 7 runs, 10000 loops each)
>>> d = list(range(100000))
>>> random.shuffle(d)
>>> %timeit np.argsort(d)[-3:]
20.4 ms ± 396 µs per loop (mean ± std. dev. of 7 runs, 10 loops each)
>>> %timeit np.argpartition(d, -3)[-3:]
12.4 ms ± 128 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)
>>> d = list(range(10000000))
>>> random.shuffle(d)
>>> %timeit np.argsort(d)[-3:]
1.71 s ± 5.1 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)
>>> %timeit np.argpartition(d, -3)[-3:]
81.4 ms ± 48.8 µs per loop (mean ± std. dev. of 7 runs, 10 loops each)
```
排序数量小时，两者相差不多，数量大了后，argpartition快很多。值得注意的是argpartition返回结果并未排序，如需要对返回结果排序，则还得进行第二次排序。综上所述：
  - 使用argsort情况：n比较小，且需要返回结果排序
  - 使用argpartition：n很大或者不需要对返回结果排序
