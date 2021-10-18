# 内置函数

## 内置函数

### enumerate()

> enumerate() 函数用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中

#### 语法

```python
# sequence：一个序列、迭代器或其他支持迭代对象
# star：下标起始位置
enumerate(sequence, [start=0])
```

#### 实例

```python
seq = ['one', 'two', 'three']
for i, element in enumerate(seq):
    print(i, element)
    
>>> 0 one
>>> 1 two
>>> 2 three
```

### random()

#### random.choice(list)

```python
random.choice(range(5))

# >>> 1 # 生成随机1~4
```
