# 常量

空值 nan

```python
numpy.nan 
numpy.NaN 
numpy.NAN
numpy.nan != numpy.nan
# 判空。 isnan(10) == False
```

极大值 inf

```python
numpy.Inf
numpy.inf  
numpy.infty 
numpy.Infinity
numpy.PINF
```

圆周率 pi

```python
numpy.pi
```

自然常数 e

```python
numpy.e
```



# 基本数据类型

| 类型                              | 备注                     | 说明       | 字符                   | 其他 |
| --------------------------------- | ------------------------ | ---------- | ---------------------- | ---- |
| bool_ = bool8                     | 8位                      | 布尔类型   | b1                     |      |
| int8 = byte                       | 8位                      | 整型       | 'i1', 'i2', 'i4', 'i8' |      |
| int16 = short                     | 16位                     | 整型       |                        |      |
| int32 = intc                      | 32位                     | 整型       |                        |      |
| int_ = int64 = long = int0 = intp | 64位                     | 整型       |                        |      |
| uint8 = ubyte                     | 8位                      | 无符号整型 | 'u1', 'u2' ,'u4' ,'u8' |      |
| uint16 = ushort                   | 16位                     | 无符号整型 |                        |      |
| uint32 = uintc                    | 32位                     | 无符号整型 |                        |      |
| uint64 = uintp = uint0 = uint     | 64位                     | 无符号整型 |                        |      |
| float16 = half                    | 16位                     | 浮点型     | 'f2', 'f4', 'f8'       |      |
| float32 = single                  | 32位                     | 浮点型     |                        |      |
| float_ = float64 = double         | 64位                     | 浮点型     |                        |      |
| str_ = unicode_ = str0 = unicode  | \|Unicode 字符串         |            |                        |      |
| datetime64                        | \|日期时间类型           |            |                        |      |
| timedelta64                       | \|表示两个时间之间的间隔 |            |                        |      |

```python
import numpy as np

a = np.dtype('b1')
print(a.type)  # <class 'numpy.bool_'>
print(a.itemsize)  # 1

a = np.dtype('i1')
print(a.type)  # <class 'numpy.int8'>
print(a.itemsize)  # 1
a = np.dtype('i2')
print(a.type)  # <class 'numpy.int16'>
```



# 日期与时间

## datetime64

### 创建

```python
import numpy as np

a = np.datetime64('2020-03-01')
print(a, a.dtype)  # 2020-03-01 datetime64[D]

a = np.datetime64('2020-03')
print(a, a.dtype)  # 2020-03 datetime64[M]

a = np.datetime64('2020-03-08 20:00:05')
print(a, a.dtype)  # 2020-03-08T20:00:05 datetime64[s]

a = np.datetime64('2020-03-08 20:00')
print(a, a.dtype)  # 2020-03-08T20:00 datetime64[m]

a = np.datetime64('2020-03-08 20')
print(a, a.dtype)  # 2020-03-08T20 datetime64[h]

```

### 指定单位

```python
a = np.datetime64('2020-03', 'D')
print(a, a.dtype)  # 2020-03-01 datetime64[D]

a = np.datetime64('2020-03', 'Y')
print(a, a.dtype)  # 2020 datetime64[Y]

print(np.datetime64('2020-03') == np.datetime64('2020-03-01'))  # True
print(np.datetime64('2020-03') == np.datetime64('2020-03-02'))  #False
```



### 生成日期范围

```python
# arange()创建 datetime64数组
a = np.arange('2020-08-01', '2020-08-10', dtype=np.datetime64)
print(a)
# ['2020-08-01' '2020-08-02' '2020-08-03' '2020-08-04' '2020-08-05'
#  '2020-08-06' '2020-08-07' '2020-08-08' '2020-08-09']
print(a.dtype)  # datetime64[D]
```

## tiemdelta64

timedelta64 表示两个 datetime64 之间的差

```python 
a = np.datetime64('2020-03-08') - np.datetime64('2020-03-07')
print(a, a.dtype)  # 1 days timedelta64[D]

a = np.datetime64('2020-03') + np.timedelta64(20, 'D')
b = np.datetime64('2020-06-15 00:00') + np.timedelta64(12, 'h')
print(a, a.dtype)  # 2020-03-21 datetime64[D]
print(b, b.dtype)  # 2020-06-15T12:00 datetime64[m]

a1 = np.datetime64('2020-03') - np.timedelta64(20, 'D')
b1 = np.datetime64('2020-06-15 00:00') - np.timedelta64(12, 'h')
print(a1, a1.dtype)  # 2020-02-10 datetime64[D]
print(b1, b1.dtype)  # 2020-06-14T12:00 datetime64[m]
```



### 工作日

busday_offset、is_busday

```python

# 2020-07-10 星期五
a = np.busday_offset('2020-07-10', offsets=1)
print(a)  # 2020-07-13

# 2020-07-10 星期五
a = np.is_busday('2020-07-10')
b = np.is_busday('2020-07-11')
print(a)  # True
print(b)  # False
```

统计工作日天数

```python
a = np.arange('2023-08-01', '2023-09-10', dtype=np.datetime64)
print(np.is_busday(a))
b = np.count_nonzero(np.is_busday(a))
print(b) # 29

# 2020-07-10 星期五
begindates = np.datetime64('2020-07-10')
enddates = np.datetime64('2020-07-20')
a = np.busday_count(begindates, enddates)
b = np.busday_count(enddates, begindates)
print(a)  # 6
print(b)  # -6
```

# 数组

ndarry类型

## arry

```python
# 一维数组
a = np.array([0, 1, 2, 3, 4])
b = np.array((0, 1, 2, 3, 4))
print(a, type(a))
# [0 1 2 3 4] <class 'numpy.ndarray'>
print(b, type(b))
# [0 1 2 3 4] <class 'numpy.ndarray'>

# 二维
c = np.array([[11, 12, 13, 14, 15],
              [16, 17, 18, 19, 20],
              [21, 22, 23, 24, 25],
              [26, 27, 28, 29, 30],
              [31, 32, 33, 34, 35]
             ])
# 三维
d = np.array([
    [(1.5, 2, 3), (4, 5, 6)],
    [(3, 2, 1), (4, 5, 6)]
             ])

```

## asarray

`array()`和`asarray()`主要区别就是当数据源是**ndarray** 时，`array()`仍然会 copy 出一个副本，占用新的内存，但不改变 dtype。 `asarray()`不会。





## fromfunction

给函数绘图的时候可能会用到`fromfunction()`，该函数可从函数中创建数组。

```python
import numpy as np

def fun1(x, y):
    return 10 * x + y

x = np.fromfunction(fun1, (5, 4), dtype=int)
print(x)
# [[ 0  1  2  3]
#  [10 11 12 13]
#  [20 21 22 23]
#  [30 31 32 33]
#  [40 41 42 43]]

x = np.fromfunction(lambda i, j: i == j, (3, 3), dtype=int)
print(x)
# [[ True False False]
#  [False  True False]
#  [False False  True]]

x = np.fromfunction(lambda i, j: i + j, (3, 3), dtype=int)
print(x)
# [[0 1 2]
#  [1 2 3]
#  [2 3 4]]
```

## zeros 、ones、empty

在机器学习任务中经常做的一件事就是初始化参数，需要用常数值或者随机值来创建一个固定大小的矩阵。

零数组-zeros，zeros_like

```python
import numpy as np

x = np.zeros(5)
print(x)  # [0. 0. 0. 0. 0.]
x = np.zeros([2, 3])
print(x)
# [[0. 0. 0.]
#  [0. 0. 0.]]

x = np.array([[1, 2, 3], [4, 5, 6]])
y = np.zeros_like(x)
print(y)
# [[0 0 0]
#  [0 0 0]]
```

1数组-ones、ones_like

```python
import numpy as np

x = np.ones(5)
print(x)  # [1. 1. 1. 1. 1.]
x = np.ones([2, 3])
print(x)
# [[1. 1. 1.]
#  [1. 1. 1.]]

x = np.array([[1, 2, 3], [4, 5, 6]])
y = np.ones_like(x)
print(y)
# [[1 1 1]
#  [1 1 1]]
```

空数组-empty，empty_like

empty()函数：返回一个空数组，数组元素为随机数。
empty_like函数：返回与给定数组具有相同形状和类型的新数组。

```python
import numpy as np

x = np.empty(5)
print(x)
# [1.95821574e-306 1.60219035e-306 1.37961506e-306 
#  9.34609790e-307 1.24610383e-306]

x = np.empty((3, 2))
print(x)
# [[1.60220393e-306 9.34587382e-307]
#  [8.45599367e-307 7.56598449e-307]
#  [1.33509389e-306 3.59412896e-317]]

x = np.array([[1, 2, 3], [4, 5, 6]])
y = np.empty_like(x)
print(y)
# [[  7209029   6422625   6619244]
#  [      100 707539280       504]]
```

