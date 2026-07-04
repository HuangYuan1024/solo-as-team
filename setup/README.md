# solo-as-team 依赖 skill 安装指引

本 skill 在 Step 1/2/5 依赖三个基础 skill，它们需要从 **Trae skill 市场**单独下载安装。

---

## 依赖清单

| 依赖 skill | 用于步骤 | 市场搜索名 | 必需性 |
|-----------|---------|-----------|--------|
| `brainstorming` | Step 1 头脑风暴 | brainstorming | 必需（无 HARD-GATE 约束则设计质量无保障） |
| `writing-plans` | Step 2 实施计划 | writing-plans | 必需（无小步粒度和占位符检查则计划不可执行） |
| `doc-coauthoring` | Step 5 文档回补 | doc-coauthoring | 推荐（无读者测试则文档可读性无保障） |

---

## 安装方式

### 方式一：Trae 客户端市场（推荐）

1. 打开 Trae 客户端
2. 进入 skill 市场或 skill 管理入口
3. 分别搜索 `brainstorming`、`writing-plans`、`doc-coauthoring`
4. 逐个点击下载/安装

### 方式二：手动安装

如果市场不可用，可从其他已安装的机器复制以下目录到本机的 `~/.trae-cn/skills/` 下：

```
~/.trae-cn/skills/brainstorming/    # 含 SKILL.md + scripts/ + 配套 prompt
~/.trae-cn/skills/writing-plans/    # 含 SKILL.md + plan-document-reviewer-prompt.md
~/.trae-cn/skills/doc-coauthoring/  # 含 SKILL.md
```

---

## 安装验证

安装完成后，solo-as-team 启动工作流时会自动检查这三个 skill 是否存在。若全部已安装，不再提示；若有缺失，会列出缺失项并暂停工作流。

也可手动检查：

```powershell
# Windows PowerShell
Test-Path "$env:USERPROFILE\.trae-cn\skills\brainstorming\SKILL.md"
Test-Path "$env:USERPROFILE\.trae-cn\skills\writing-plans\SKILL.md"
Test-Path "$env:USERPROFILE\.trae-cn\skills\doc-coauthoring\SKILL.md"
```

```bash
# macOS / Linux
test -f ~/.trae-cn/skills/brainstorming/SKILL.md && echo "brainstorming OK"
test -f ~/.trae-cn/skills/writing-plans/SKILL.md && echo "writing-plans OK"
test -f ~/.trae-cn/skills/doc-coauthoring/SKILL.md && echo "doc-coauthoring OK"
```

三条命令都返回 True / OK 即安装成功。

---

## 缺失时的降级处理

若某项 skill 暂时无法安装，用户可告知 solo-as-team 在缺失状态下运行，工作流会切换到简化降级流程：

- 缺 `brainstorming`：Step 1 改为直接对话式澄清需求，但无 HARD-GATE 约束
- 缺 `writing-plans`：Step 2 改为输出简化任务清单，无小步粒度和占位符检查
- 缺 `doc-coauthoring`：Step 5 改为直接按模板填写文档，无读者测试环节

降级流程会明确告知质量保障降低，建议尽快补装缺失 skill。

---

## 为什么不打包进 solo-as-team

三个基础 skill 是 Trae 市场维护的独立 skill，会持续更新。打包成静态副本会导致：
1. 三个 skill 无法被 Trae 正常识别和独立触发（skill 发现机制要求扁平目录）
2. 与已安装的同名 skill 冲突
3. 无法享受官方更新

因此采用"依赖检查 + 市场下载"的方式，保持各 skill 独立可更新。