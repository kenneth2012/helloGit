# TDD 脚手架

生成 TDD 测试脚手架的指南。

## TDD 脚手架生成流程

### 1. 分析需求

```markdown
## 需求分析

### 功能
[功能描述]

### 输入
- 参数 1: 类型, 描述
- 参数 2: 类型, 描述

### 输出
- 返回值: 类型, 描述

### 边界情况
- [ ] 空输入
- [ ] 最小值
- [ ] 最大值
- [ ] 错误输入
```

### 2. 生成测试文件结构

```python
# tests/test_<module>.py

import pytest
from module import function


class TestFunction:
    """功能测试组"""

    def test_function_with_valid_input(self):
        """测试有效输入"""
        pass

    def test_function_with_empty_input(self):
        """测试空输入"""
        pass

    def test_function_with_invalid_input(self):
        """测试无效输入"""
        pass
```

### 3. 测试用例模板

```python
# 正常情况
def test_<name>_success():
    """测试成功场景"""
    result = function(valid_input)
    assert result == expected

# 边界情况
def test_<name>_edge_case():
    """测试边界情况"""
    pass

# 错误情况
def test_<name>_error():
    """测试错误情况"""
    with pytest.raises(ErrorType):
        function(invalid_input)
```

## 测试覆盖率目标

| 测试类型 | 目标覆盖率 |
|----------|-----------|
| 核心函数 | 100% |
| 辅助函数 | 80% |
| 边界处理 | 100% |
| 错误处理 | 100% |

## 测试文件命名

```
tests/
├── unit/
│   ├── test_module.py
│   └── test_utils.py
├── integration/
│   └── test_api.py
└── conftest.py  # 共享 fixtures
```

## Fixtures 示例

```python
# conftest.py
import pytest

@pytest.fixture
def sample_user():
    return {
        "name": "Alice",
        "email": "alice@example.com"
    }

@pytest.fixture
def sample_users():
    return [
        {"name": "Alice", "email": "alice@example.com"},
        {"name": "Bob", "email": "bob@example.com"}
    ]
```
