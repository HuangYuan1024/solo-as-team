# solo-as-team 个人即团队

> 一个人 + AI = 一个完整的开发团队

一套经过实战验证的、基于 Trae 的 AI 辅助开发工作流 Skill，让个人开发者借助 AI 完成原本需要产品、设计、开发、测试、文档等多个角色协作的全流程工作，覆盖 **需求 -> 设计 -> 计划 -> 审查 -> 开发 -> 测试 -> 文档** 的全生命周期。

## 核心理念

**AI 不是替代某个角色，而是让一个人能同时扮演所有角色。流程纪律 + 工程规则是保证质量的关键--团队靠协作制衡，个人靠流程制衡。**

## 工作流总览（6 步闭环 + 计划审查闸门）

```
0. 需求 -> 1. 头脑风暴 -> 2. 实施计划 -> 2.5 计划审查 -> 3. 开发与测试 -> 4. 人工测试 -> 5. 文档回补
   ↑                                                                                    │
   └──────────────────────── 复盘产生新需求，回到 Step 0 ←───────────────────────────────┘
```

| 步骤 | 主导 | 调用 Skill | 产出 |
|------|------|-----------|------|
| 0. 需求收集 | 人 + AI | - | 需求文档（req/），含验收 checklist |
| 1. 头脑风暴 | AI | `brainstorming` | 设计方案（spec/），含降级矩阵 + 设计审查清单 |
| 2. 实施计划 | AI | `writing-plans` | 实施计划（plan/） |
| 2.5 计划审查 | AI | - | 审查修正记录（两轮，P0/P1/P2 分级） |
| 3. 开发与测试 | AI | `test-driven-development` + `executing-plans` + `git-commit` | 代码 + 自动化测试 + 规范提交 |
| 4. 人工测试 | 人 | - | 逐条复用 Step 0 验收 checklist |
| 5. 文档回补 | AI | `doc-coauthoring` | spec 回补 + note 提炼 + 日报 |

### 流程级 TDD（测试驱动开发）

本 skill 的核心创新：TDD 的本质不是"写测试"，而是**"先定义会失败的验收标准，再做实现，最后验证标准被满足"**。这套思路从代码层提升到流程层：

- Step 0 写验收 checklist（Red）
- Step 1 写降级矩阵和审查清单（Red）
- Step 2.5 做两轮计划审查（Red）
- Step 3 写单元测试（Red，传统 TDD）
- Step 4 逐条复用 Step 0 的验收 checklist（Red 变 Green）

每阶段的"绿"都对应前一阶段的"红"被消除，形成贯穿全流程的验收链。详见 [SKILL.md](SKILL.md) 第一章 1.1 节。

## 前置依赖

本 skill 在 Step 1/2/3/5 依赖六个基础 skill，需从 **Trae skill 市场**单独下载安装：

| 依赖 skill | 用于步骤 | 作用 |
|-----------|---------|------|
| `brainstorming` | Step 1 头脑风暴 | HARD-GATE 防止跳过设计 |
| `writing-plans` | Step 2 实施计划 | 禁止占位符保证计划可执行 |
| `test-driven-development` | Step 3 TDD 铁律 | watch it fail 防止测试流于形式 |
| `executing-plans` | Step 3 stop-and-ask 协议 | 撞墙即停，防止硬猜 |
| `git-commit` | Step 3 提交规范 | Conventional Commits + Git 安全协议 |
| `doc-coauthoring` | Step 5 文档回补 | 读者测试保证文档可读 |

详见 [setup/README.md](setup/README.md)。skill 启动时会自动检查这六个依赖是否已安装，缺失则提示下载，并提供简化降级流程。

## 安装方式

### 方式一：git clone（推荐）
以下命令操作可由AI帮忙做

```bash
git clone https://github.com/HuangYuan1024/solo-as-team.git
```

把目录复制到 Trae skills 目录：

```bash
# Windows
cp -r solo-as-team %USERPROFILE%\.trae-cn\skills\

# macOS / Linux
cp -r solo-as-team ~/.trae-cn/skills/
```

### 方式二：Trae 客户端导入

1. 下载本仓库为 ZIP 并解压
2. 打开 Trae 客户端
3. 进入 skill 管理入口，选择"导入插件"
4. 选中解压后的 `solo-as-team` 文件夹

### 安装验证

启动 Trae 后，在工作流相关对话中会自动触发本 skill。也可在 skill 列表中确认 `solo-as-team` 已出现。

## 设计原则

本 skill 内置以下工程规则（从实战复盘提炼，详见 [SKILL.md](SKILL.md) 第三章）：

### 工程方法

- **流程级 TDD（测试驱动开发）**：验收先行，每阶段都遵循 Red-Green-Refactor
- **分步验证**：功能拆为最小步骤，每步立即测试，禁止多步堆积后统一测试
- **两轮审查**：计划审查必须做两轮，第一轮按维度清单查问题，第二轮查上一轮修正引入的副作用
- **降级优先**：先设计失败场景和降级路径，增强功能失败不阻断主流程
- **复用优先**：新增代码前排查现有能力是否可复用
- **最小改动**：只做必要改动，保持 diff 可审
- **契约不变**：重构时保持对外接口不变，只改内部实现
- **配置驱动**：可变参数走配置，不硬编码
- **遗留待办不丢**：不能立即修复的问题记成待办表，传递到后续 Task 和文档回补
- **文件操作铁律**：先迁移 -> 再验证 -> 后删除（不可逆操作的三步铁律）

### 开发纪律（Step 3）

- **TDD 铁律**：NO PRODUCTION CODE WITHOUT A FAILING TEST FIRST（没有失败测试就不写生产代码）
- **watch it fail 强制**：写完测试必须先运行确认它失败，且失败原因正确
- **stop-and-ask 协议**：遇到 blocker（测试反复失败、依赖缺失、指令歧义、验证失败超 2 次）立即停下问人，不硬猜
- **Conventional Commits**：type/scope/description + 现在时祈使句 + <72 字符，一个逻辑改动一个 commit
- **Git 安全协议**：永不改 config、永不 --force、永不 --no-verify、永不 force push main、永不提交密钥

### 健壮性与性能

- **并发状态机防竞态**：状态机中间态用独立标志位 + 锁限制并发
- **高频小写入用攒批异步**：30s 攒批后台写入，降低 DB 压力
- **配置热加载范式**：可热加载走 runtime_config，不可热加载走 settings
- **单一数据源原则**：同一计数器/状态不内存和 DB 双写

## 适用场景

- 个人开发者使用 Trae 进行全栈项目开发
- 希望 AI 辅助但不愿牺牲工程质量的开发者
- 需要可复用、可追溯的开发流程的独立开发者/自由职业者
- 生产级系统开发（含限流、熔断、审计、多租户等非功能性要求）

## 使用示例
跟Trae对话时，可以输入 `/solo-as-team` 手动调skill。也可以跟Trae说你要加新功能，需要进行需求分析和系统设计，他大概会自动调用skill，实在不行就手动调。

## 仓库结构

```
solo-as-team/
├── SKILL.md              # 主 skill（6步流程 + 计划审查 + 流程级TDD + 工程规则 + 文档规范）
├── setup/
│   └── README.md         # 依赖 skill 安装指引（6 个基础 skill）
├── README.md             # 本文件
├── LICENSE               # MIT 协议
└── .gitignore
```

## 贡献

欢迎提 Issue 和 PR。本 skill 会持续迭代，欢迎分享你的实战案例。

## 许可证

[MIT](LICENSE)
