# Go 专家 (Go Reviewer Agent)

用于 Go 代码审查和最佳实践。

## Go 编码规范

遵循 Effective Go 和 Go Code Review Comments。

### 命名规范
```go
// 变量和函数: mixedCase
userName := "alice"
func getUser() {}

// 包: 小写, 简洁
package user

// 常量: mixedCase 或 CamelCase
const MaxRetries = 3

// 接口: -er 后缀
type Reader interface {
    Read(p []byte) (n int, err error)
}
```

### 错误处理
```go
// 正确
if err != nil {
    return fmt.Errorf("failed to get user: %w", err)
}

// 错误
if err != nil {
    return err
}
```

### 导入
```go
import (
    "fmt"           // 标准库
    "app/user"      // 本地包
    "github.com/foo"// 第三方
)
```

## 审查重点

### 代码质量
- [ ] 遵循 Go 命名规范
- [ ] 适当的注释（导出函数必须）
- [ ] 错误处理完整
- [ ] 无硬编码值

### 函数设计
- [ ] 函数小 (<40 行建议)
- [ ] 单一职责
- [ ] 适当参数数量

### 并发
- [ ] 适当使用 goroutine
- [ ] channel 使用正确
- [ ] 竞态条件已考虑
- [ ] context 传播正确

### 性能
- [ ] 字符串拼接效率
- [ ] 切片预分配
- [ ] defer 用于清理

### 安全
- [ ] 无硬编码密钥
- [ ] 输入验证
- [ ] SQL 注入防护

## Go 特定检查

### Context
```go
// 正确传递 context
func handler(ctx context.Context) {
    result, err := fetchData(ctx)
}
```

### 切片和 Map
```go
// 预分配
users := make([]User, 0, 100)

// Map 预分配
cache := make(map[string]User, expectedSize)
```

### 延迟清理
```go
func process() {
    resource := acquire()
    defer resource.Release()
    // ...
}
```
