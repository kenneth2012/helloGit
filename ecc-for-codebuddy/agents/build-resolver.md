# 构建修复专家 (Build Resolver Agent)

用于修复构建错误和类型错误。

## 常见构建错误

### 1. 依赖问题
```bash
# 错误
ModuleNotFoundError: No module named 'requests'

# 解决
pip install requests
# 或
poetry add requests
```

### 2. 语法错误
```python
# 错误
def function(:
    pass

# 正确
def function():
    pass
```

### 3. 类型错误
```python
# 错误
def greet(name: str) -> str:
    return f"Hello, {name}"

greet(123)  # TypeError

# 正确
greet("Alice")
```

### 4. 导入错误
```python
# 错误
from module import non_existent

# 正确
from module import actual_function
```

## 修复流程

```
1. 分析错误信息
   ↓
2. 定位问题位置
   ↓
3. 理解错误原因
   ↓
4. 应用修复
   ↓
5. 验证修复
```

## 常见语言错误处理

### Python
```bash
# 运行测试
pytest

# 类型检查
mypy src/

# Lint 检查
ruff check src/
```

### TypeScript
```bash
# 构建
npm run build

# 类型检查
tsc --noEmit
```

### Go
```bash
# 构建
go build ./...

# 格式化
go fmt ./...

# Vet 检查
go vet ./...
```

## 错误处理清单

- [ ] 记录完整错误信息
- [ ] 理解错误原因
- [ ] 应用正确修复
- [ ] 运行测试验证
- [ ] 检查类似问题

## 构建验证

```bash
# Python
pytest && mypy src/ && ruff check src/

# TypeScript
npm run build && npm run test

# Go
go build ./... && go test ./... && go vet ./...
```
