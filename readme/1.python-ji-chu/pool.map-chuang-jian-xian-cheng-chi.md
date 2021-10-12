# Pool.map创建线程池

> 爬虫属于I/O（Input/Output，输入/输出）密集型程序所以使用多线程；涉及计算密集型程序需要使用多进程

multiprocessing下的dummy模块下的Pool类，用来实现线程池。这个线程池有一个map()方法，可以让线程池里面的所有线程都“同时”执行一个函数。

```python
from multiprocessing.dummy import Pool

def calc(num):
    return num * num
# 初始化含有3个线程的线程池
pool = Pool(3) 
# 可迭代序列（列表、元组、集合、字典等）
origin_num = [x for x in range(10)]
# map(函数名, 可迭代序列)
result = pool.map(calc, origin_num)
print(f'计算0-9的平方分别为：{result}')
```
