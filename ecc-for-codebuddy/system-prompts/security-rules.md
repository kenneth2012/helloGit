# 安全规则

安全是不可妥协的。

## 关键安全检查

### 提交前必须验证

1. **无硬编码密钥**
   - API keys
   - 密码
   - Tokens
   - 私钥

2. **输入验证**
   - 所有用户输入必须验证
   - 使用模式验证
   - 快速失败

3. **SQL 注入防护**
   - 使用参数化查询
   - 从不使用字符串拼接 SQL

4. **XSS 防护**
   - 净化 HTML 输出
   - 使用安全的 DOM 操作

5. **CSRF 保护**
   - 所有状态变更操作启用 CSRF 保护

6. **身份验证/授权**
   - 验证每个请求的身份
   - 检查权限

7. **速率限制**
   - 所有端点必须有速率限制

8. **错误处理**
   - 错误消息不泄露敏感数据
   - 记录详细日志（服务端）

## 密钥管理准则

```python
# 错误 ❌
api_key = "sk-1234567890abcdef"

# 正确 ✅
api_key = os.environ.get("API_KEY")
if not api_key:
    raise ValueError("API_KEY environment variable is required")
```

## 安全审查清单

- [ ] 所有输入已验证
- [ ] 使用参数化查询
- [ ] 输出已净化
- [ ] CSRF 保护已启用
- [ ] 身份验证已实现
- [ ] 授权检查已实现
- [ ] 速率限制已配置
- [ ] 无敏感数据泄露

## 发现安全问题的处理流程

1. **STOP** — 立即停止当前操作
2. **SECURITY REVIEW** — 使用 security-reviewer 进行全面审查
3. **FIX CRITICAL** — 优先修复关键问题
4. **ROTATE SECRETS** — 如果密钥暴露，立即轮换
5. **SCAN CODEBASE** — 检查代码库中是否有类似问题
6. **DOCUMENT** — 记录问题和修复方案
