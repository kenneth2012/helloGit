# 安全扫描

安全漏洞扫描指南。

## 扫描范围

### 1. 硬编码密钥
```bash
# 检查常见密钥模式
grep -r "api_key\|password\|secret\|token" --include="*.py" --include="*.js"
```

### 2. SQL 注入
```python
# 不安全 ❌
query = f"SELECT * FROM users WHERE id = {user_id}"

# 安全 ✅
query = "SELECT * FROM users WHERE id = %s"
cursor.execute(query, (user_id,))
```

### 3. XSS 漏洞
```python
# 不安全 ❌ - 直接输出用户输入
html = f"<div>{user_input}</div>"

# 安全 ✅ - 净化输入
import bleach
html = f"<div>{bleach.clean(user_input)}</div>"
```

### 4. 敏感数据暴露
```python
# 不安全 ❌
return {"user": user, "password": password}

# 安全 ✅
return {"user": user}  # 不返回密码
```

## 扫描流程

```
1. 静态分析 - 检查代码模式
   ↓
2. 依赖扫描 - 检查已知漏洞
   ↓
3. 配置审查 - 检查安全配置
   ↓
4. 报告生成 - 输出安全报告
```

## 常用工具

| 工具 | 用途 | 命令 |
|------|------|------|
| Bandit | Python 安全 | `bandit -r ./src` |
| ESLint | JS 安全 | `eslint --security` |
| npm audit | Node 依赖 | `npm audit` |
| safety | Python 依赖 | `safety check` |

## 安全报告模板

```markdown
## 安全扫描报告

### 扫描时间
[时间]

### 扫描范围
- [文件/目录]

### 发现问题

#### 严重 🔴
| 位置 | 描述 | 修复建议 |
|------|------|----------|
| [文件:行号] | [描述] | [建议] |

#### 中等 🟡
| 位置 | 描述 | 修复建议 |
|------|------|----------|
| [文件:行号] | [描述] | [建议] |

### 总体评估
[评估]

### 建议
- [ ]
```
