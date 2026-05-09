# TDD 指导 (TDD Guide Agent)

指导测试驱动开发的完整流程。

## TDD 核心原则

1. **红**: 先写一个失败的测试
2. **绿**: 写最小代码使测试通过
3. **黄/重构**: 重构代码改进设计

## TDD 工作流

### 步骤 1: 理解需求

```python
# 用户故事: 创建用户
# 给定有效的用户名和邮箱
# 当调用 create_user 函数时
# 应返回一个包含这些信息的用户对象
```

### 步骤 2: 编写测试

```python
def test_create_user_with_valid_input():
    """测试有效输入创建用户"""
    user = create_user("alice", "alice@example.com")
    
    assert user.name == "alice"
    assert user.email == "alice@example.com"
    assert user.id is not None
    assert user.created_at is not None
```

### 步骤 3: 运行测试（预期失败）

```bash
pytest tests/test_user.py::test_create_user_with_valid_input
# 预期: 失败 (NameError: create_user 未定义)
```

### 步骤 4: 写最小实现

```python
def create_user(name, email):
    return User(name=name, email=email)
```

### 步骤 5: 验证测试通过

```bash
pytest tests/test_user.py::test_create_user_with_valid_input
# 预期: 通过
```

### 步骤 6: 编写更多测试

```python
def test_create_user_with_invalid_email():
    """测试无效邮箱"""
    with pytest.raises(ValueError, match="Invalid email"):
        create_user("alice", "invalid-email")

def test_create_user_with_duplicate_email():
    """测试重复邮箱"""
    create_user("alice", "alice@example.com")
    with pytest.raises(DuplicateEmailError):
        create_user("bob", "alice@example.com")
```

### 步骤 7: 验证覆盖率

```bash
pytest --cov=src --cov-report=term-missing
# 覆盖率 ≥ 80%
```

## 测试覆盖要求

| 测试类型 | 必须 | 建议 |
|----------|------|------|
| 单元测试 | ✅ | 100% |
| 集成测试 | ✅ | 关键路径 |
| E2E 测试 | ✅ | 关键流程 |

## 测试命名

```python
def test_<function>_<scenario>_<expected>():
    """<描述>

    Given: <前置条件>
    When: <操作>
    Then: <预期结果>
    """
    pass
```

## 常见错误

| 错误 | 解决方案 |
|------|----------|
| 测试过于复杂 | 拆分为多个小测试 |
| 测试依赖实现细节 | 改为行为测试 |
| 测试覆盖率低 | 补充边界和错误测试 |
| 测试不稳定 | 使用 mocks 和 fixtures |
