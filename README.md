# 错误和异常



## 错误和异常

### 捕 获异常

#### 捕获所有异常

> Exception是所有程序异常类的父亲

```python
try:
    print(num)
# #Exception可以将所有的异常包括在内
except Exception as result:
    print(result)
```

