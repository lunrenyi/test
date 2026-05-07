# x-cmd install YML 字段说明

> 本文档详细说明了 x-cmd install 元数据仓库中 yml 文件的字段结构。

---

## 字段概览

### 必需字段

| 字段 | 类型 | 说明 | 示例 |
|------|------|------|------|
| `lang` | string | 编程语言 | `lang: Go` |
| `homepage` | string | 项目主页 URL | `homepage: https://github.com/jqlang/jq` |
| `desc` | object | 描述（中英文双语） | 见下方详解 |
| `rule` | object | 安装规则 | 见下方详解 |

---

## 必需字段详解

### lang

声明软件包主要使用的编程语言。

```yaml
lang: Go
```

常用值：C、C++、Go、Rust、Python、JavaScript、TypeScript、Shell、Bash、Ruby、Java、Kotlin、Swift、Zig、OCaml、Perl、Racket、Lua、Haskell、Scala、C#、Dart、Elixir、Erlang、Nim、R、Julia

### homepage

项目的官方主页或 GitHub 仓库 URL。

```yaml
homepage: https://github.com/jqlang/jq
```

### desc

软件包的双语描述。

**字段结构：**
```yaml
desc:
  cn: 中文描述
  en: English description
```

**示例：**
```yaml
desc:
  cn: jq 是一个轻量级且灵活的命令行 JSON 处理器
  en: jq is a lightweight and flexible command-line JSON processor
```

### rule

安装规则，定义软件在不同系统下的安装命令。

**字段结构：**
```yaml
rule:
  <os>/<tool>:       # 操作系统/包管理器组合
    cmd: <command>    # 安装命令
    reference: <url>  # 命令来源 URL（可选但推荐）
    dsnap: <pkg>      # Debian 快照包名（可选）
```

**支持的 OS/工具 组合：**

| OS | 包管理器/工具 | 示例键名 |
|----|---------------|----------|
| darwin | brew | `darwin/brew` |
| darwin | port | `darwin/port` |
| debian | apt | `debian/apt` |
| ubuntu | apt | `ubuntu/apt` |
| arch | pacman | `arch/pacman` |
| arch | yay (AUR) | `arch/yay` |
| alpine | apk | `alpine/apk` |
| fedora | dnf | `fedora/dnf` |
| opensuse | zypper | `opensuse/zypper` |
| freebsd | pkg | `freebsd/pkg` |
| nix | - | `nix/` |
| void | xbps | `void/xbps` |
| gentoo | emerge | `gentoo/emerge` |
| (win\|wsl2) | scoop | `(win\|wsl2)/scoop` |
| (win\|wsl2) | choco | `(win\|wsl2)/choco` |
| (win\|wsl2) | winget | `(win\|wsl2)/winget` |
| mint | pip | `mint/pip` |
| chrome | crew | `chrome/crew` |
| 通用 | pip | `/pip` |
| 通用 | cargo | `/cargo` |
| 通用 | go | `/go` |
| 通用 | asdf | `/asdf` |
| 通用 | curl | `/curl` |

**rule.cmd 多行命令格式：**
```yaml
rule:
  ubuntu/apt:
    cmd: |
      sudo apt update \
      && sudo apt install python3-dev python3-pip \
      && pip3 install thefuck --user
    reference: https://github.com/nvbn/thefuck#installation
```

**dsnap 字段说明：**
当 Debian/Ubuntu 系统包名与软件名不同时使用。例如 `git-delta` 包的软件名是 `delta`。

**示例：**
```yaml
rule:
  darwin/brew:
    cmd: brew install jq
    reference: https://formulae.brew.sh/formula/jq#default

  debian/apt:
    cmd: sudo apt-get install jq
    reference: https://command-not-found.com/jq
    dsnap: jq

  arch/pacman:
    cmd: sudo pacman -S jq
    reference: https://wiki.archlinux.org/title/Jq

  /cargo:
    cmd: cargo install jq
    reference: https://github.com/jqlang/jq/releases
    dsnap: jq
```

---

## 完整 yml 文件示例

```yaml
lang: Go
homepage: https://github.com/jqlang/jq

desc:
  cn: jq 是一个轻量级且灵活的命令行 JSON 处理器
  en: jq is a lightweight and flexible command-line JSON processor

rule:
  darwin/brew:
    cmd: brew install jq
    reference: https://formulae.brew.sh/formula/jq#default

  debian/apt:
    cmd: sudo apt-get install jq
    reference: https://command-not-found.com/jq
    dsnap: jq

  ubuntu/apt:
    cmd: sudo apt-get install jq
    reference: https://command-not-found.com/jq
    dsnap: jq

  arch/pacman:
    cmd: sudo pacman -S jq
    reference: https://wiki.archlinux.org/title/Jq

  /cargo:
    cmd: cargo install jq
    reference: https://github.com/jqlang/jq/releases
    dsnap: jq

  (win|wsl2)/scoop:
    cmd: scoop install jq
    reference: https://scoop.sh/#/apps?q=jq
```

---

## 常见问题

**Q: 如何确定应该使用哪个分类？**
A: 参考 [分类指南](./CATEGORIES.md)，按软件的主要功能进行分类。

**Q: reference 字段是必填的吗？**
A: 不是必填，但推荐填写，以便审核人员验证安装命令的正确性。

**Q: 一个软件支持多个系统的安装命令，可以只填一个吗？**
A: 可以。rule 字段支持任意数量的系统/工具组合，填写常见的系统即可。
