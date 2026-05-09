# TDD 工作流

测试驱动开发是强制要求。

## 测试覆盖率要求

**最低覆盖率: 80%**

## 测试类型

1. **单元测试** — 独立函数、工具、组件
2. **集成测试** — API 端点、数据库操作
3. **端到端测试** — 关键用户流程

## TDD 工作流（强制）

### 步骤 1: 写测试（RED）

```python
def test_user_creation():
    # 先写测试
    user = create_user("alice", "alice@example.com")
    assert user.name == "alice"
    assert user.email == "alice@example.com"
```

### 步骤 2: 写最小实现（GREEN）

```python
def create_user(name, email):
    return User(name=name, email=email)
```

### 步骤 3: 重构（IMPROVE）

验证覆盖率 ≥ 80%，持续改进代码质量。

## 每个任务的 TDD 流程

1. 理解需求
2. 写测试用例（覆盖正常、边界、错误情况）
3. 运行测试（应该失败 - RED）
4. 写最小实现（GREEN）
5. 重构并确保测试通过（REFACTOR）
6. 验证测试覆盖率
7. 提交代码

## 测试命名规范

```python
def test_<function_name>_<scenario>_<expected_result>():
    pass

# 示例
def test_user_creation_with_valid_email_succeeds():
    pass

def test_user_creation_with_invalid_email_raises_error():
    pass

def test_user_creation_with_duplicate_email_raises_error():
    pass
```

## 故障排除

测试失败时：
1. 检查测试隔离
2. 验证 mocks
3. 修复实现（非测试，除非测试本身错误）

## 自动测试命令

```bash
# 运行所有测试
pytest

# 运行带覆盖率的测试
pytest --cov=. --cov-report=html

# 运行特定文件的测试
pytest tests/test_user.py

# 运行上次失败的测试
pytest --lf
```
