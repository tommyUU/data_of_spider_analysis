## NumPy创建数组

```python
numpy.array(object,dtype = None,copy = True,order = None,subok = False,ndmin = 0)
# 使用array方法创建参数
```

### 参数


| 序号 | 参数   | 描述说明                                                            |
| ------ | -------- | --------------------------------------------------------------------- |
| 1    | object | 表示一个数组序列                                                    |
| 2    | dtype  | 可选参数，通过它可以更改数组的数据类型                              |
| 3    | copy   | 可选参数，当数据源是`ndarray`时表示数组能否被复制，默认是`True`                    |
| 4    | order  | 可选参数，以哪种内存布局创建数组，有3个可选值，分别是`C（行序列`）/`F（列序列）`/`A（默认）`           |
| 5    | ndmin  | 可选参数，用于指定数组的维度                                        |
| 6    | subok  | 可选参数，类型为`bool`值，默认`False`。为`True`使用`object`的内部数据类型；`False`:使用`object`数组的数据类型 |

# 引入numpy


```python
# 注意默认都会给numpy包设置别名为np
import numpy as np
```

# array创建数组：


```python
# array(函数，括号内可以是列表、元祖、数组、迭代对象，生成器
np.array([1,2,3,4,5])
```


    array([1, 2, 3, 4, 5])



# 检查对象类型

## 列表


```python
a = np.array ([1,2,3,4,5])
print(a)
type(a)
```

    [1 2 3 4 5]

    numpy.ndarray



## 元组


```python
np.array((1,2,3,4,5))
```


    array([1, 2, 3, 4, 5])




```python
type(np.array((1,2,3,4,5)))
```


    numpy.ndarray



## 数组


```python
a=np.array([1,2,3,4,5])
print(a)
type(a)
```

    [1 2 3 4 5]

    numpy.ndarray



## 迭代对象


```python
a = np.array(range(10))
print(a)
type(a)
```

    [0 1 2 3 4 5 6 7 8 9]

    numpy.ndarray



## 生成器


```python
a = np.array([i**2 for i in range(10)])
print(a)
type(a)
```

    [ 0  1  4  9 16 25 36 49 64 81]

    numpy.ndarray



# 创建10以内的偶数数组


```python
# np.array(range(2,11,2))
np.array([i for i in range(10) if i%2 ==0])
```


    array([0, 2, 4, 6, 8])




```python
# 列表中元素类型不相同
np.array([1,1.5,3,4.5,'5'])
```


    array(['1', '1.5', '3', '4.5', '5'], dtype='<U32')




```python
ar1 = np.array(range(10)) # 整型
ar1
```


    array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])




```python
ar2 = np.array([1,2,3.14,4,5]) # 浮点型
ar2
```


    array([1.  , 2.  , 3.14, 4.  , 5.  ])




```python
ar3 =np.array([
            [1,2,3],
            ('a','b','c')
            ]) # 二维数组：嵌套序列(列表，元祖均可)
ar3
```


    array([['1', '2', '3'],
           ['a', 'b', 'c']], dtype='<U21')




```python
# 注意嵌套序列数量不一会怎么样
ar4 = np.array([[1,2,3],('a','b','c','d')])
ar4
```

    array([list([1, 2, 3]), ('a', 'b', 'c', 'd')], dtype=object)



# 查看ar4的维度


```python
ar4.ndim
```


    1



# 查看ar4的行数


```python
ar4.shape
```


    (2,)




```python
# 注意嵌套序列数量不一会怎么样
ar4 = np.array([[1,2,3],[1,2,3,4]])
ar4
```

    array([list([1, 2, 3]), list([1, 2, 3, 4])], dtype=object)



## 强制转换 设置dtype参数，默认自动识别


```python
a = np.array([1, 2, 3, 4, 5])
print(a)

# 设置数组元素类型
a = np.array([1, 2, 3, 4, 5], dtype='float')
print(a)
```

    [1 2 3 4 5]
    [1. 2. 3. 4. 5.]


## 思考如何将浮点型的数据，设置为整形，会是什么情况？


```python
np.array([1.1,2.5,3.8,4,5],dtype='int')
# 强制转换为int
# 向下取整
```


    array([1, 2, 3, 4, 5])



## 拷贝，设置copy参数，默认True


```python
a = np.array([1,2,3,4,5])
# 定义b,复制a
b = np.array(a)
# 输出a和b的id
print('a:' ,id(a), 'b:', id(b))
print('以上看出a和b的内存地址')
```

    a: 140183674856400 b: 140183674855056
    以上看出a和b的内存地址



```python
# 当修改b的元素时，a不会发生变化
b[0] =10
print('a:',a,'\nb:',b)
```

    a: [1 2 3 4 5] 
    b: [10  2  3  4  5]


### array方法是直接在内存中开辟新的内存地址，而不是简单的指向同样的内存地址。数据量很大，使用array会极大浪费内存地址


```python
a = np.array([1,2,3,4,5])
# 直接等于，是试图操作，相当于列表的引用赋值
b = a 
# 输出a和b的id
print('a:',id(a), 'b:',id(b))
print('以上看出a和b的内存地址')
```

    a: 140183674858320 b: 140183674858320
    以上看出a和b的内存地址


## ndmin用于指定数组的维度


```python
a = np.array([1,2,3])
print(a)
a = np.array([1,2,3],ndmin=2)
a
```

    [1 2 3]

    array([[1, 2, 3]])



### 一维表用`[]`,二维表用`[[]]` 以此类推

## subok参数，类型为`bool`值，默认`False`。为`True`,使用`object`的内部数据类型；`False`:使用数组的数据类型


```python
# 创建一个矩阵
a = np.mat([1,2,3,4])
# 输出为矩阵类型
print(type(a))
# 既要复制一份刷本，又要保持原类型
at = np.array (a, subok=True)
af = np.array(a) # 默认为False
print ('at,subok为True:', type(at))
print ('af,subok为False:', type (af))
print(id(at),id(a))
```

    <class 'numpy.matrix'>
    at,subok为True: <class 'numpy.matrix'>
    af,subok为False: <class 'numpy.ndarray'>
    139707047713472 139707066138176


### 书写代码是需要注意的内容：


```python
# 定义个数组
a = np.array([2,4,3,1])
# 在定义b时，如果想复制a的几种方案：

# 1.使用np.array()
b = np.array(a)
print('b =np.array(a):', id(b), id(a))

# 2.使用数组的copy()方法
c =a.copy()
print('c = a.copy():', id(c), id(a))

# 注意不能直接使用=号复制，直接使用=号，会使2个变量指向相同的内存地址
d = a
# 修改d也会相应的修改a
print('d =a:', id(d), id(a))
```

    b =np.array(a): 139707048168784 139707048169648
    c = a.copy(): 139707048168976 139707048169648
    d =a: 139707048169648 139707048169648


## 练习

> * 创健一个一维数组
> * 创建一个二维数组
> * 创建嵌套序列数量不一样的数组，查看结果
> * 测试数组，将数组赋值给部，修改b中的一个元素，查看a是否变化
> * 紧接看4如果想让b变化不影响a,如何实现
