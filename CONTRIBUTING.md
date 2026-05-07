# x-cmd install 贡献指南

感谢您对 x-cmd install 元数据仓库的关注！本仓库包含 ~1658 个软件包的安装元数据，分布在 69 个模块目录下。

---

## 目录

- [快速开始](#快速开始)
- [贡献方式概述](#贡献方式概述)
- [Issue 贡献（新手友好）](#方式一issue-贡献新手友好)
- [PR 贡献（推荐）](#方式二pr-贡献推荐)
- [YML 文件结构](#yml-文件结构)
- [分类规则](#分类规则)
- [PR 标题格式](#pr-标题格式)
- [标签系统](#标签系统)
- [常见问题](#常见问题)

---

## 快速开始

### 1. 找到对应的分类目录

软件包按功能分类存放在 `src/` 目录下的各个模块中。例如：

| 软件类型 | 目录 |
|----------|------|
| 系统监控工具 | `src/osman/` |
| Git 工具 | `src/scm-git-tool/` |
| 网络工具 | `src/network/` |
| 终端工具 | `src/terminal/` |
| 编程语言 | `src/lang/`, `src/lang-python/` 等 |

### 2. 创建或修改 yml 文件

```yaml
# src/reader/delta.yml 示例
lang: rust
homepage: https://github.com/dandavison/delta

desc:
  cn: 用于 git、diff 和 grep 输出的语法高亮分页器
  en: A syntax-highlighting pager for git, diff, and grep output

rule:
  darwin/brew:
    cmd: brew install git-delta
    reference: https://github.com/dandavison/delta#installation

  debian/apt:
    cmd: sudo apt install git-delta
    reference: https://github.com/dandavison/delta#installation

  arch/pacman:
    cmd: sudo pacman -S git-delta
    reference: https://github.com/dandavison/delta#installation
```

### 3. 详细文档

- [YML 字段完整说明](./docs/YML_SCHEMA.md)
- [分类规则详解](./docs/CATEGORIES.md)
- [AI 自动填写指南](./docs/AUTO_FILL_PROMPT.md)

---

## 贡献方式概述

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│   方式一：Issue 贡献（新手友好）                              │
│   └─ 适合：不熟悉 Git / 只想贡献一个包                        │
│                                                             │
│   方式二：PR 贡献（推荐）                                    │
│   └─ 适合：熟悉 Git / 贡献多个包 / 希望快速响应               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## 方式一：Issue 贡献（新手友好）

```
贡献者
   │
   ├─→ 访问仓库 GitHub 页面
   │
   ├─→ 点击 "Issues" → "New Issue"
   │
   ├─→ 选择 Issue 模板（添加包 / 更新信息 / 报告问题）
   │
   ├─→ 填写表单
   │      ├─ 包名称
   │      ├─ 官网/仓库链接
   │      ├─ 分类
   │      ├─ 描述（中英文）
   │      └─ 安装命令
   │
   └─→ 提交 Issue

              ▼

         Bot 自动检查
         ├─ 必填项是否完整？
         ├─ 安装命令格式是否正确？
         └─ 仓库链接是否可访问？

              ▼
         ┌────┴────┐
         │ 通过？   │
         └────┬────┘
          Yes │ No
              ▼    ▼
         ┌──────────┐    ┌─────────────────┐
         │ Bot 自动  │    │ Bot 回复：缺失   │
         │ 生成 PR   │    │ xxx 字段，请补全 │
         └──────────┘    └─────────────────┘

              ▼

         维护者 Review

              ▼

         ┌──────────┐
         │ 通过？    │
         └────┬─────┘
          Yes │ No
              ▼    ▼
         ┌────────┐    ┌─────────────────┐
         │ Merge  │    │ 反馈问题，关闭   │
         └────────┘    └─────────────────┘
```

### Issue 模板说明

| 模板 | 用途 |
|------|------|
| [提交新软件包](.github/ISSUE_TEMPLATE/add-package.yml) | 提交一个新的软件包到仓库 |
| [更新软件包信息](.github/ISSUE_TEMPLATE/update-package.yml) | 更新已有软件包的描述、安装命令等 |
| [报告问题](.github/ISSUE_TEMPLATE/bug-report.yml) | 报告软件包安装问题 |

---

## 方式二：PR 贡献（推荐）

```
贡献者
   │
   ├─→ Fork 仓库到自己的 GitHub 账号
   │
   ├─→ Clone 到本地
   │
   ├─→ 创建新分支（建议命名：add/xxx-package）
   │
   ├─→ 添加或修改 yml 文件
   │      └─ 参考文档填写字段
   │
   ├─→ 本地调试验证（如有本地工具）
   │
   ├─→ 提交 commit
   │      └─ 标题格式：add: 新增 xxx 包
   │
   ├─→ Push 到自己的 Fork
   │
   └─→ 在 GitHub 上创建 PR
          └─ 使用 PR 模板填写变更说明
          └─ 可参考 [AI 自动填写指南](./docs/AUTO_FILL_PROMPT.md) 让 AI 帮您生成 yml

              ▼

         PR 自动检查（Bot + CI）
         ├─ yml 格式校验
         ├─ 字段完整性检查
         ├─ 安装命令有效性检查
         └─ CI 测试

              ▼

         维护者 Review + Merge

              ▼

         包正式上线
```

---

## YML 文件结构

### 必需字段

| 字段 | 类型 | 说明 |
|------|------|------|
| `lang` | string | 编程语言，如 Go、Rust、Python |
| `homepage` | string | 项目主页 URL |
| `desc` | object | 描述，必须包含 `cn`（中文）和 `en`（英文） |
| `rule` | object | 安装规则 |

### rule 字段格式

```yaml
rule:
  <os>/<tool>:       # 如 darwin/brew, debian/apt, arch/pacman
    cmd: <command>    # 安装命令（必填）
    reference: <url> # 参考链接（必填）
    dsnap: <pkg>      # Debian 快照包名（可选）
```

详见：[YML 字段完整说明](./docs/YML_SCHEMA.md)

---

## 分类规则

本仓库使用 37 个功能分类：

| 分类 | 说明 | 分类 | 说明 |
|------|------|------|------|
| ai | AI 工具 | osman | 系统监控 |
| build | 编译构建 | package-manager | 包管理 |
| cicd | CI/CD | programming | 编程通用 |
| container | 容器 | reader | 阅读器 |
| container-kube | Kubernetes | scm | 版本控制 |
| data-* | 数据处理 | security | 安全 |
| db* | 数据库 | shell | Shell 增强 |
| filesystem | 文件系统 | ssh | SSH 工具 |
| lang* | 编程语言 | terminal | 终端 |
| network | 网络 | test | 测试 |
| cloud | 云服务 | virtualization | 虚拟化 |
| editor | 编辑器 | web* | Web 相关 |

详见：[分类规则详解](./docs/CATEGORIES.md)

---

## PR 标题格式

```
add: 新增 xxx 包              # 新增包
update: 更新 xxx 包信息       # 更新已有包
fix: 修复 xxx 包安装命令      # 修复错误
```

---

## 标签系统

| 标签 | 用途 |
|------|------|
| `new-package` | 新增包 |
| `update` | 更新信息 |
| `bug-fix` | 修复错误 |
| `question` | 提问 |

---

## 流程对比

| 维度 | Issue 贡献 | PR 贡献 |
|------|-----------|---------|
| 门槛 | 低（填表单） | 中（需懂 Git） |
| 响应速度 | 较慢（等 Bot + 维护者） | 快（社区并行处理） |
| 适合场景 | 新手 / 一次性贡献 | 活跃贡献者 / 多包 |
| 维护者工作量 | 高（Bot 辅助写 PR） | 低（只 Review） |

---

## 常见问题

### Q: 如何确定软件包应该放在哪个目录？

A: 参考 [分类规则](./docs/CATEGORIES.md)，根据软件的主要功能进行分类。如果无法确定，可以使用 `misc`（杂项）或在 Issue 中询问。

### Q: 安装命令需要填写所有系统吗？

A: 不需要，填写常见的系统即可（如 darwin/brew、debian/apt、arch/pacman）。

### Q: reference 字段是必填的吗？

A: 是的，`reference` 字段是必填的。请提供安装命令的官方文档或权威来源链接。

### Q: desc 必须用中文吗？

A: 是的，`desc` 必须同时包含 `cn`（中文）和 `en`（英文）。

### Q: 可以一次提交多个软件包吗？

A: 可以，但建议每个 PR 只包含一个软件包的变更，以便于审核。

---

## 相关链接

- [GitHub 仓库](https://github.com/x-cmd/x-cmd-install)
- [YML 字段说明](./docs/YML_SCHEMA.md)
- [分类规则](./docs/CATEGORIES.md)
