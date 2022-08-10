# Crash问题-常见crash原因总结

### 1 Dev

#### 内存非法访问

- 访问空指针
- 访问野指针
- 越界访问等
- segment error，bus error等

#### OpenCV报错

- MAT error，如copyTo、imwrite错误使用等

#### 逻辑断言终止

- 如FAIL_EXIT，abort()等

#### 算术运算异常

- 如分母为零

### 2 外部

- 传递非法指针等，如output_data
- 外部内存踩踏，导致crash在dev等（需要细究）

### 3 内部

- 调用库崩库等