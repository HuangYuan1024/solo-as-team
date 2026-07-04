# solo-as-team 个人即团队

> 一个人 + Trae AI = 一个完整的开发团队

一套经过实战验证的、基于 Trae 的 AI 辅助开发工作流 Skill，让个人开发者借助 AI 完成原本需要产品、设计、开发、测试、文档等多个角色协作的全流程工作，覆盖 **需求 → 设计 → 实施 → 测试 → 文档** 的全生命周期。

## 核心理念

**AI 不是替代某个角色，而是让一个人能同时扮演所有角色。流程纪律 + 工程规则是保证质量的关键——团队靠协作制衡，个人靠流程制衡。**

## 工作流总览（6 步闭环）

```
0. 需求收集与确认 → 1. 头脑风暴 → 2. 实施计划 → 3. 开发与测试 → 4. 人工测试 → 5. 文档回补
                     ↑                                                              │
                     └──────────── 复盘产生新需求，回到 Step 0 ←─────────────────────┘
```

| 步骤 | 主导 | 调用 Skill | 产出 |
|------|------|-----------|------|
| 0. 需求收集 | 人 + AI | — | 需求文档（req/） |
| 1. 头脑风暴 | AI | `brainstorming` | 设计方案（spec/） |
| 2. 实施计划 | AI | `writing-plans` | 实施计划（plan/） |
| 3. 开发与测试 | AI | — | 代码 + 自动化测试 |
| 4. 人工测试 | 人 | — | UX/视觉/回归验证 |
| 5. 文档回补 | AI | `doc-coauthoring` | spec 回补 + note 提炼 + 日报 |

## 前置依赖

本 skill 在 Step 1/2/5 依赖三个基础 skill，需从 **Trae skill 市场**单独下载安装：

- `brainstorming`（Step 1 头脑风暴）
- `writing-plans`（Step 2 实施计划）
- `doc-coauthoring`（Step 5 文档回补）

详见 [setup/README.md](setup/README.md)。skill 启动时会自动检查这三个依赖是否已安装，缺失则提示下载。

## 安装方式

### 方式一：git clone（推荐）

```bash
git clone https://github.com/你的用户名/solo-as-team.git
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

## 使用示例

见 [examples/ai-chatbot案例.md](examples/ai-chatbot案例.md)——记录了本工作流在 AI 智能客服项目（ai-chatbot）上的实战应用，含 DOCX 预览改进、Lightbox 交互增强、视频理解全链路等功能的完整开发过程。

## 仓库结构

```
solo-as-team/
├── SKILL.md              # 主 skill（6步流程 + 工程规则 + 文档规范）
├── setup/
│   └── README.md         # 依赖 skill 安装指引
├── examples/
│   └── ai-chatbot案例.md  # 实战案例
├── README.md             # 本文件
├── LICENSE               # MIT 协议
└── .gitignore
```

## 设计原则

本 skill 内置以下工程规则（从实战复盘提炼）：

- **分步验证**：功能拆为最小步骤，每步立即测试，禁止多步堆积后统一测试
- **降级优先**：先设计失败场景和降级路径，增强功能失败不阻断主流程
- **复用优先**：新增代码前排查现有能力是否可复用
- **最小改动**：只做必要改动，保持 diff 可审
- **契约不变**：重构时保持对外接口不变，只改内部实现
- **配置驱动**：可变参数走配置，不硬编码
- **文件操作铁律**：先迁移 → 再验证 → 后删除（不可逆操作的三步铁律）

## 适用场景

- 个人开发者使用 Trae 进行全栈项目开发
- 希望 AI 辅助但不愿牺牲工程质量的开发者
- 需要可复用、可追溯的开发流程的独立开发者/自由职业者

## 贡献

欢迎提 Issue 和 PR。本 skill 会持续迭代，欢迎分享你的实战案例。

## 许可证

[MIT](LICENSE)