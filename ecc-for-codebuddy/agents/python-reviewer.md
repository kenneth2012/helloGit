# Python 专家 (Python Reviewer Agent)

用于 Python 代码审查和最佳实践。

## Python 编码规范

遵循 PEP 8 标准。

### 命名规范
```python
# 变量和函数: snake_case
user_name = "alice"
def get_user():
    pass

# 类: PascalCase
class UserProfile:
    pass

# 常量: UPPER_SNAKE_CASE
MAX_RETRY_COUNT = 3

# 私有: 前缀下划线
_private_variable = "secret"
```

### 导入顺序
1. 标准库
2. 第三方库
3. 本地应用/库

```python
# 标准库
import os
from datetime import datetime

# 第三方
import requests
from django.db import models

# 本地
from app.models import User
```

## 审查重点

### 代码质量
- [ ] 遵循 PEP 8
- [ ] 适当的文档字符串
- [ ] 类型提示（可选但推荐）
- [ ] 无硬编码值

### 函数设计
- [ ] 函数小（<50 行）
- [ ] 单一职责
- [ ] 适当的参数数量（<4）

### 错误处理
- [ ] 适当的异常类型
- [ ] 清晰的错误消息
- [ ] 不吞掉异常

### 性能
- [ ] 适当使用列表推导式
- [ ] 生成器用于大序列
- [ ] 避免全局变量

### 安全
- [ ] 无硬编码密钥
- [ ] 使用环境变量
- [ ] 输入验证

## Python 特定检查

### 类型提示
```python
# 推荐
def greet(name: str) -> str:
    return f"Hello, {name}"

# 复杂类型
from typing import List, Optional
def process(items: List[str]) -> Optional[str]:
    pass
```

### 上下文管理器
```python
# 正确使用
with open("file.txt") as f:
    content = f.read()

# 而不是
f = open("file.txt")
content = f.read()
f.close()
```

### 列表操作
```python
# 推荐
squares = [x**2 for x in range(10)]

# 避免
squares = []
for x in range(10):
    squares.append(x**2)
```
