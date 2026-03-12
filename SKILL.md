---
name: mob-programming
description: |
  组建 Pair/Mob Programming 团队进行代码开发。根据用户需求智能选择团队配置：
  - Pair 模式（2人）：Turing（测试）+ Thompson（实现），内部遵循 TDD 规范
  - Pair 审查模式（2人）：Jobs（Navigator）+ Thompson（Driver），内部遵循 SOLID 原则
  - Mob 三人模式（3人）：Turing + Jobs + Thompson，完整双重审查流程

  触发场景：
  - "pair programming" / "结对编程" / "结对" → 询问选择 Pair 模式
  - "mob programming" / "团队编程" → 启动三人模式
  - "代码审查" / "帮我重构" → Pair 审查模式
  - 提到 "Turing/Jobs/Thompson" → 按指定角色启动

triggers:
  - "pair programming"
  - "结对编程"
  - "结对"
  - "pair"
  - "mob programming"
  - "团队编程"
  - "代码审查"
  - "重构"
  - "Turing"
  - "Jobs"
  - "Thompson"
---

# Pair/Mob Programming Skill

## 核心原则（TDD + SOLID）

### TDD 三法则
1. **RED**: 先写测试，后写实现
2. **GREEN**: 只写让测试通过的最少代码
3. **IMPROVE**: 重构优化，保持测试通过

### SOLID 检查清单
- **S**ingle Responsibility: 一个函数只做一件事
- **O**pen/Closed: 对扩展开放，对修改关闭
- **L**iskov Substitution: 子类可替换父类
- **I**nterface Segregation: 接口小而专注
- **D**ependency Inversion: 依赖抽象而非具体

---

## 模式选择（必须询问用户）

**当用户说 "pair programming" / "结对编程" / "结对" 时，必须询问：**

> "请选择 Pair Programming 模式：
> 1. **Pair 开发模式** (Turing + Thompson): 测试专家编写测试，实现专家编写代码（内部遵循 TDD 规范）
> 2. **Pair 审查模式** (Jobs + Thompson): 架构师指导，实现专家编码（内部遵循 SOLID 原则）"

**当用户说 "mob programming" 时，说明：**
> "将启动三人团队 (Turing + Jobs + Thompson)，包含完整测试方案→审查→实现→审查流程"

---

## 团队配置

### Pair 开发模式 👥（内部遵循 TDD 规范）

```yaml
配置: Turing + Thompson
适用场景: 新功能开发
内部规范: TDD（测试驱动开发）
工作流程:
  1. Turing: 分析需求 → 编写测试方案
  2. Turing: 编写测试代码 (RED)
  3. Thompson: 执行测试 (确认失败) → 编写生产代码 (GREEN)
  4. Thompson: 重构优化 (IMPROVE)
  5. 循环直到功能完成

TDD循环:
  - 小步快跑：每个测试 < 5分钟实现
  - 测试隔离：每个测试独立可运行
  - 持续集成：频繁运行全部测试
```

### Pair 审查模式 👥（内部遵循 SOLID 原则）

```yaml
配置: Jobs (Navigator) + Thompson (Driver)
适用场景: 代码重构、复杂逻辑实现、质量把关
内部规范: SOLID 原则
工作流程:
  1. Jobs: 分析现有代码 → 制定重构/实现方案
  2. Thompson: 按方案编写代码
  3. Jobs: 实时审查 → 提出改进建议
  4. Thompson: 修改代码
  5. 循环直到 Jobs 批准

审查重点 (SOLID):
  - S: 函数是否只做一件事？
  - O: 是否需要抽象/接口？
  - L: 继承关系是否正确？
  - I: 接口是否被污染？
  - D: 是否依赖具体实现？
```

### Mob 三人模式 👥👤

```yaml
配置: Turing + Jobs + Thompson
适用场景: 关键功能、高风险变更、团队培训
工作流程:
  1. Turing: 编写测试方案
  2. Jobs: 审查测试方案
  3. Turing: 编写测试代码
  4. Jobs: 审查测试代码
  5. Thompson: 执行测试 → 编写生产方案
  6. Jobs: 审查生产方案
  7. Thompson: 编写生产代码
  8. Jobs: 审查生产代码
  9. 循环直到完成

质量保证:
  - 双重审查：测试和代码都需通过审查
  - 架构把关：Jobs 确保符合设计原则
  - 测试覆盖：Turing 确保 80%+ 覆盖率
```

---

## 启动流程

### Step 1: 识别需求

分析用户输入，选择模式：

```
用户说 "pair programming" / "结对编程" / "结对" → 询问选择 开发模式 或 审查模式
用户说 "mob programming" / "团队编程" → 默认三人模式
用户说 "代码审查" / "帮我重构" → Pair 审查模式
```

**重要**：TDD 和 SOLID 是内部遵循的规范，不是触发条件。无论哪种模式，内部都严格执行相应的代码质量标准。

### Step 2: 任务拆解

将需求拆分为子任务（每个 < 100行代码）：

```
示例：用户注册功能
├── [Turing] 用户名验证测试
├── [Thompson] 用户名验证实现
├── [Turing] 密码强度检查测试
├── [Thompson] 密码强度检查实现
├── [Turing] 邮箱格式验证测试
├── [Thompson] 邮箱格式验证实现
└── [Turing/Thompson] 集成测试
```

### Step 3: 启动团队

**Pair 开发模式：**
```
TeamCreate(name: "pair-dev-{task}", members: [Turing, Thompson])
```

**Pair 审查模式：**
```
TeamCreate(name: "pair-review-{task}", members: [Jobs, Thompson])
```

**Mob 三人模式：**
```
TeamCreate(name: "mob-{task}", members: [Turing, Jobs, Thompson])
```

---

## 工作流程详情

### Pair 开发详细流程（内部遵循 TDD 规范）

```
┌─────────────┐     ┌─────────────┐
│   Turing    │     │  Thompson   │
│  (测试专家)  │◄───►│  (实现专家)  │
└──────┬──────┘     └──────┬──────┘
       │                   │
       ▼                   │
1. 编写测试方案             │
       │                   │
       ▼                   │
2. 编写测试代码 (RED)       │
       │                   │
       ├──────────────────►│
       │                   ▼
       │              3. 执行测试
       │                   │
       │              4. 编写实现 (GREEN)
       │                   │
       │              5. 重构 (IMPROVE)
       │                   │
       │◄──────────────────┤
       ▼                   │
6. 审查测试覆盖            │
       │                   │
       ▼                   │
7. 下一个测试...           │
```

### Pair 审查详细流程

```
┌─────────────┐     ┌─────────────┐
│    Jobs     │     │  Thompson   │
│  (Navigator)│◄───►│   (Driver)  │
└──────┬──────┘     └──────┬──────┘
       │                   │
       ▼                   │
1. 分析代码/需求           │
       │                   │
       ▼                   │
2. 制定实现方案            │
       │                   │
       ├──────────────────►│
       │                   ▼
       │              3. 编写代码
       │                   │
       │◄──────────────────┤
       ▼                   │
4. SOLID审查              │
   ├─ S: 单一职责？         │
   ├─ O: 开闭原则？         │
   ├─ L: 里氏替换？         │
   ├─ I: 接口隔离？         │
   └─ D: 依赖倒置？         │
       │                   │
   通过? ──Yes──► 完成     │
    No                      │
    │                       │
    └──────────────────────►│
                      5. 修改代码
                            │
                            └───────┐
                                    │
                            返回步骤 4
```

---

## 角色分工（严格遵守）

### Turing - 测试专家

**职责：**
- ✅ 编写测试方案
- ✅ 编写测试代码
- ✅ 确保测试覆盖率 80%+
- ✅ 维护测试质量

**禁止：**
- ❌ 编写生产代码
- ❌ 修改生产代码文件
- ❌ 直接审查生产代码

**检查清单：**
```
□ 测试覆盖正常路径
□ 测试覆盖边界情况
□ 测试覆盖错误处理
□ 测试命名清晰
□ 遵循 Arrange-Act-Assert 模式
□ 测试之间相互独立
```

### Thompson - 实现专家

**职责：**
- ✅ 执行测试（RED 阶段）
- ✅ 编写生产代码（GREEN 阶段）
- ✅ 重构优化（IMPROVE 阶段）
- ✅ 确保所有测试通过

**禁止：**
- ❌ 编写测试代码
- ❌ 修改测试方案
- ❌ 跳过 RED 阶段直接写代码

**检查清单：**
```
□ 只写让测试通过的最少代码
□ 遵循 SOLID 原则
□ 函数长度 < 50 行
□ 参数数量 < 4 个
□ 处理所有错误情况
□ 命名清晰表达意图
```

### Jobs - 架构师/审查者

**职责：**
- ✅ 审查设计方案
- ✅ 审查代码质量
- ✅ 确保符合 SOLID 原则
- ✅ 提供改进建议

**禁止：**
- ❌ 编写测试代码
- ❌ 编写生产代码
- ❌ 直接修改任何代码

**审查清单：**
```
□ 功能完整性
□ SOLID 原则合规性
□ 命名规范
□ 代码可读性
□ 错误处理完善
□ 代码重复检查
□ 性能考虑
□ 语言惯用法
```

---

## TDD 循环规范

### RED 阶段规范

```go
// 测试先写，明确期望行为
func TestCalculator_Add_TwoNumbers(t *testing.T) {
    // Arrange
    calc := NewCalculator()
    a, b := 2, 3
    expected := 5

    // Act
    result := calc.Add(a, b)

    // Assert
    if result != expected {
        t.Errorf("Add(%d, %d) = %d, want %d", a, b, result, expected)
    }
}
```

**要求：**
1. 测试在实现之前编写
2. 测试必须失败（验证测试有效性）
3. 失败信息清晰明确

### GREEN 阶段规范

```go
// 最少代码让测试通过
func (c *Calculator) Add(a, b int) int {
    return a + b  // 最简单的实现
}
```

**要求：**
1. 只写让测试通过的代码
2. 不添加额外功能
3. 不预优化
4. 硬编码可以接受（暂时）

### IMPROVE 阶段规范

```go
// 重构后：支持更多运算
func (c *Calculator) Add(a, b int) (int, error) {
    result := a + b
    if result > MaxInt {
        return 0, ErrOverflow
    }
    return result, nil
}
```

**重构原则：**
1. 不改变外部行为
2. 提高代码质量
3. 所有测试保持通过
4. 小步前进

---

## SOLID 应用指南

### S - 单一职责

```go
// ❌ 坏：一个函数做太多事
func ProcessUser(user User) {
    validate(user)
    saveToDB(user)
    sendEmail(user)
    logActivity(user)
}

// ✅ 好：每个函数只做一件事
func ValidateUser(user User) error { ... }
func SaveUser(user User) error { ... }
func NotifyUser(user User) error { ... }
func LogUserActivity(user User) { ... }
```

### O - 开闭原则

```go
// ❌ 坏：修改现有代码来扩展
type PaymentProcessor struct { ... }
func (p *PaymentProcessor) Process(method string) {
    if method == "wechat" { ... }
    if method == "alipay" { ... }
}

// ✅ 好：通过接口扩展
 type PaymentMethod interface {
    Process(amount float64) error
}

type WechatPay struct{}
func (w *WechatPay) Process(amount float64) error { ... }

type Alipay struct{}
func (a *Alipay) Process(amount float64) error { ... }
```

### L - 里氏替换

```go
// 子类应该能替换父类而不改变行为
type Bird interface {
    Fly() error
}

// ❌ 坏：企鹅不能飞
type Penguin struct{}
func (p *Penguin) Fly() error {
    return errors.New("penguins can't fly")
}

// ✅ 好：分离接口
type Bird interface {
    Move() error
}

type FlyingBird interface {
    Bird
    Fly() error
}
```

### I - 接口隔离

```go
// ❌ 坏：大而全的接口
type Worker interface {
    Work()
    Eat()
    Sleep()
}

// ✅ 好：小而专注的接口
type Worker interface {
    Work()
}

type Eater interface {
    Eat()
}

type Sleeper interface {
    Sleep()
}
```

### D - 依赖倒置

```go
// ❌ 坏：依赖具体实现
type OrderService struct {
    db *MySQLDatabase  // 具体依赖
}

// ✅ 好：依赖抽象
type Database interface {
    Get(id string) (Order, error)
    Save(order Order) error
}

type OrderService struct {
    db Database  // 依赖接口
}
```

---

## 降级处理

### 当 Agent/Team 工具权限不足

**什么情况会触发降级？**
- Claude Code 尝试调用 `Agent` 或 `TeamCreate` 工具时
- 用户的权限设置不允许使用多 Agent 功能
- 系统提示权限不足或工具不可用

**此时立即切换到手动协调模式：**

```
1. 向用户说明："Agent工具权限不足，我将直接为您执行 Pair/Mob Programming 流程"
2. 根据选择的模式，我（主Agent）按顺序执行：
   - Pair 开发模式: 先执行 Turing 的测试工作（RED），再执行 Thompson 的实现工作（GREEN→IMPROVE）
   - Pair 审查模式: 先以 Jobs 视角审查，再以 Thompson 视角实现
3. 严格按照 RED → GREEN → IMPROVE 流程
4. 每步执行代码质量检查清单
```

**注意**：降级后仍保持角色分工的概念，只是由主 Agent 顺序执行，而非并行启动多个子 Agent。

---

## 输出规范

### 每个 TDD 循环结束时报告

```
=== TDD 循环 #{n} ===
[RED] 测试: TestXXX
      状态: 失败（预期）
      错误: [错误信息]

[GREEN] 实现: [函数名]
        状态: 通过
        代码行数: X行

[IMPROVE] 重构: [改进点]
          状态: 完成
          测试状态: 全部通过 ✓

=== SOLID 检查 ===
[S] 单一职责: ✓
[O] 开闭原则: ✓
[L] 里氏替换: N/A
[I] 接口隔离: ✓
[D] 依赖倒置: ✓

下一步: [继续下一个测试/完成任务]
```

---

## 开始工作

等待用户输入，根据关键词识别模式：
- "pair programming" / "结对编程" / "结对" → 询问 开发/审查 模式
- "mob programming" / "团队编程" → 启动三人模式
- "代码审查" / "重构" → Pair 审查模式

**注意**：TDD 和 SOLID 是 Pair/Mob Programming 团队内部遵循的开发规范，不是外部触发词。
