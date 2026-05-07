# x-cmd install 分类规则

> 本文档说明了 x-cmd install 元数据仓库的软件包分类规则。

---

## 分类原则

1. **按主要功能分类**：根据软件的主要用途或所属领域进行分类
2. **单一分类**：每个软件只能属于一个分类，避免重复
3. **特殊分类**：无法明确归类时使用 `etc`（其他）分类
4. **一致性**：x-cmd-install 与 x-cmd-pkg 的分类必须保持一致

---

## 37 个分类说明

| 分类 | 说明 | 示例软件 |
|------|------|----------|
| **ai** | AI 服务相关的工具 | ollama, chatgpt, claude-code, lmstudio |
| **app** | 桌面应用程序 | 阿里云盘, QQ, VSCode |
| **awk** | AWK 相关工具 | gawk, mawk, nawk |
| **blockchain** | 区块链相关工具 | ethers, solana, bitcoin-cli |
| **build** | 编译构建工具 | gcc, cmake, make, ninja |
| **c++** | C++ 相关工具 | clang, clang++, libc++ |
| **cicd** | 持续集成/持续部署工具 | jenkins, github-actions, gitlab-ci |
| **cloud** | 云服务工具 | aws-cli, gcloud, azure-cli |
| **container** | 容器相关工具 | docker, podman, containerd |
| **container-kube** | Kubernetes 相关工具 | kubectl, helm, kustomize |
| **data-bin** | 二进制数据处理工具 | xxd, binwalk |
| **data-csv-tsv** | CSV/TSV 数据处理工具 | csvq, q, xsv |
| **data-json-yml** | JSON/YAML 数据处理工具 | jq, yq |
| **data-line** | 行数据处理工具 | datamash, paste, join |
| **data-text** | 文本数据处理工具 | sed, tr, cut, sort |
| **db** | 数据库通用工具 | mycli, pgcli, usql |
| **db-mysql** | MySQL 相关工具 | mysql, mysqldump, percona-toolkit |
| **db-pg** | PostgreSQL 相关工具 | psql, pg_dump, pg_restore |
| **db-sqlite** | SQLite 相关工具 | sqlite3, sqlitebrowser |
| **editor** | 文本编辑器 | vim, neovim, emacs, nano |
| **email** | 电子邮件工具 | neomutt, msmtp, sendmail |
| **entertainment** | 娱乐工具 | mpv, mplayer, youtube-dl |
| **file-disk** | 磁盘/分区管理工具 | fdisk, parted, lsblk |
| **file-manager** | 文件管理器 | ranger, fff, joshuto |
| **filesystem** | 文件系统工具 | fd, broot, tree, du |
| **finance** | 金融工具 | ledger, hledger, bank-cli |
| **font** | 字体工具 | fontconfig, fc-cache, otf2ttf |
| **iac** | 基础设施即代码工具 | terraform, pulumi, ansible |
| **input-method** | 输入法工具 | fcitx, ibus, rime |
| **journey** | 笔记/日志工具 | obsidian, joplin, trilium |
| **lang** | 编程语言（运行时环境） | node, python, ruby |
| **lang-js-ts** | JavaScript/TypeScript 工具 | deno, bun, esbuild |
| **lang-perl-raku** | Perl/Raku 工具 | perl, raku, cpan |
| **lang-python** | Python 生态工具 | pip, pipenv, poetry |
| **library** | 编程库/SDK | openssl, libcurl, zlib |
| **linter** | 代码检查工具 | eslint, golangci-lint, shellcheck |
| **log** | 日志分析工具 | lnav, multitail, glogg |
| **mac** | macOS 专用工具 | brew, mas, pbcopy |
| **markdown-html** | Markdown 处理工具 | pandoc, marked, remark |
| **misc** | 杂项工具（无法归类） | thefuck, bat, exa, procs |
| **multimedia** | 多媒体处理工具 | ffmpeg, imagemagick, sox |
| **natural-language** | 自然语言处理工具 | trans, translate-shell |
| **network** | 网络工具 | curl, wget, aria2, netcat |
| **osman** | 系统监控管理工具 | htop, neofetch, glances, btop |
| **other** | 特殊分类 | 特殊用途软件 |
| **package-manager** | 包管理工具 | apt, yum, pacman, brew |
| **programming** | 编程通用工具 | git, gh, diffutils |
| **reader** | 阅读器/TUI 工具 | delta, pandoc, mdcat |
| **scm** | 版本控制通用工具 | git, svn, mercurial |
| **scm-git-service** | Git 服务平台工具 | gh, glab, gitlab-cli |
| **scm-git-tool** | Git 工具 | lazygit, tig, git-delta |
| **scientific-computing** | 科学计算工具 | bc, dc,units, R |
| **sdkman** | SDKMAN! 生态工具 | sdkman, java, maven |
| **security** | 安全相关工具 | nmap, hydra, john, sqlmap |
| **shell** | Shell 增强工具 | zsh, fish, bash, starship |
| **ssh** | SSH 相关工具 | ssh, scp, sshfs, mux |
| **temp** | 临时/测试工具 | 临时文件处理 |
| **terminal** | 终端模拟器相关 | tmux, screen, wezterm, alacritty |
| **test** | 测试工具 | pytest, go test, jest |
| **virtualization** | 虚拟化工具 | qemu, virtualbox, vmware |
| **web** | Web 通用工具 | curl, wget, httpie |
| **web-apitool** | API 测试工具 | httpie, curl, API testing |
| **web-browser** | Web 浏览器 | chromium, firefox |
| **web-infrastructure** | Web 基础设施 | nginx, caddy, traefik |
| **web-template** | Web 模板工具 | yeoman, cookiecutter |
| **wasm** | WebAssembly 工具 | wasm-pack, wasmer, wasmtime |

---

## 分类选择指南

### 判断流程

```
1. 这个软件的主要用途是什么？
   │
   ├─ AI 相关 → ai
   │
   ├─ 编程开发
   │   ├─ 编程语言 → lang, lang-js-ts, lang-python 等
   │   ├─ 编译器/构建 → build
   │   ├─ 包管理 → package-manager
   │   ├─ 版本控制 → scm, scm-git-tool
   │   ├─ 测试 → test
   │   └─ 代码检查 → linter
   │
   ├─ 数据处理
   │   ├─ JSON/YAML → data-json-yml
   │   ├─ CSV/TSV → data-csv-tsv
   │   └─ 文本处理 → data-text, awk
   │
   ├─ 系统管理
   │   ├─ 监控 → osman
   │   ├─ 网络 → network
   │   └─ 用户/权限 → （选择最相关的）
   │
   ├─ 容器/云
   │   ├─ 容器 → container
   │   └─ Kubernetes → container-kube
   │
   ├─ 安全 → security
   │
   ├─ 终端/Shell
   │   ├─ 终端模拟器 → terminal
   │   └─ Shell 增强 → shell
   │
   └─ 其他 → misc 或 etc
```

### 示例

| 软件 | 分类 | 原因 |
|------|------|------|
| `jq` | data-json-yml | 主要用于 JSON 数据处理 |
| `fd` | filesystem | 用于文件查找，属于文件系统工具 |
| `htop` | osman | 系统监控工具 |
| `docker` | container | 容器运行时 |
| `kubectl` | container-kube | Kubernetes 命令行工具 |
| `gh` | scm-git-service | GitHub CLI，属于 Git 服务平台工具 |
| `lazygit` | scm-git-tool | Git 终端 UI 工具 |
| `delta` | reader | git diff 分页器和阅读器 |
| `glow` | markdown-html | Markdown 渲染工具 |
| `ffmpeg` | multimedia | 音视频处理 |

---

## 分类调整流程

如果需要调整某个软件包的分类：

1. 在 Issue 中说明调整原因
2. 提供新分类的建议
3. 维护者审核后进行更改

---

## 相关链接

- [YML 字段说明](./YML_SCHEMA.md)
