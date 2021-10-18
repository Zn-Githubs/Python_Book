# Module_os

## OS模块

> OS：operating system（操作系统），OS模块提供了非常丰富的方法用来处理文件和目录

### os.path模块

> os.path 模块主要用于获取文件的属性

#### 常用方法

* os.path.exists(path)：路径存在则返回True,否则返回False

### os.makedirs() 方法

> os.makedirs() 方法用于递归创建目录

语法

```python
# path：需要递归创建的目录
# mode：权限模式
os.makedirs(path[, mode=0o777
```
