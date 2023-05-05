```python
import numpy as np
```

引入`numpy`包，并给它取别名`np`


```python
np.__version__
```




    '1.23.5'



查看`numpy`的版本


```python
def python_sum(n):  # 原生python实现2个数组的加法
    # 使用列表生成式创建1到N的平方
    a = [i**2 for i in range(n)]
    # 使用列表生成式创建1到的立方
    b = [i**3 for i in range(n)]
    # 新创建新列表
    ab_sum=[]
    # 循环a的索引
    for i in range(n):
        # 将a中的对应元素与b中对应的元素相加
        ab_sum.append (a[i]+b[i])
    return ab_sum
    
```

使用纯python实现数组加法，实现的方法是用循环分支`for`


```python
# 调用实现函数
python_sum(10)
```




    [0, 2, 12, 36, 80, 150, 252, 392, 576, 810]



# 使用`numpy`实现代码


```python
def numpy_sum(n): 	# numpy实现2个数组的加法
    a = np.arange(n) ** 2
    b = np.arange (n) ** 3
    return a + b
```


```python
# 调用numpy实现函数
numpy_sum(10)
```




    array([  0,   2,  12,  36,  80, 150, 252, 392, 576, 810])



# 对比实现`1000`次


```python
%timeit python_sum(1000)
```

    578 µs ± 1.94 µs per loop (mean ± std. dev. of 7 runs, 1,000 loops each)


`python`实现


```python
%timeit numpy_sum(1000)
```

    8.5 µs ± 23.7 ns per loop (mean ± std. dev. of 7 runs, 100,000 loops each)


`numpy`实现

# 对比实现`100000`次


```python
%timeit python_sum(100000)
```

    65.5 ms ± 66.7 µs per loop (mean ± std. dev. of 7 runs, 10 loops each)



```python
%timeit numpy_sum(100000)
```

    939 µs ± 5.22 µs per loop (mean ± std. dev. of 7 runs, 1,000 loops each)


# 对比实现`100000`次


```python
%timeit python_sum(1000000)
```

    671 ms ± 1.54 ms per loop (mean ± std. dev. of 7 runs, 1 loop each)



```python
%timeit numpy_sum(1000000)
```

    11.9 ms ± 64.4 µs per loop (mean ± std. dev. of 7 runs, 100 loops each)


# 将上述结果绘图对比


```python
import pandas as pd   # 创建数据
python_times = [1.72*1000,201*1000,1.85*1000*1000]
numpy_times = [18.8,1.71*1000,17.6*1000]
```


```python
# 创建pandas的DataFrame类型数据
charts_data = pd.DataFrame({
    'python_times' :python_times,
    'numpy_times' :numpy_times,
})
```


```python
charts_data
# 单位微秒
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

```python
.dataframe tbody tr th {
    vertical-align: top;
}

.dataframe thead th {
    text-align: right;
}
```
</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>python_times</th>
      <th>numpy_times</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1720.0</td>
      <td>18.8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>201000.0</td>
      <td>1710.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1850000.0</td>
      <td>17600.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 线型图
charts_data.plot()
```
![output_25_1.png](..%2Fimage%2Foutput_25_1.png)
```python
# 柱状图
charts_data.plot.bar()
```
![output_26_1.png](..%2Fimage%2Foutput_26_1.png)