# AI 自动填写 yml 文件指南

> 使用本 prompt 让 AI 助手帮您生成符合规范的 yml 文件内容

---

## 快速开始

将下方的 prompt 复制给 AI 助手，并提供软件包的基本信息即可。

---

## Prompt

```
请帮我为 x-cmd install 元数据仓库生成一个 yml 文件。

## 软件信息
- 软件名称：<请填写>
- 官方主页：<请填写>
- 编程语言：<请填写>
- 分类目录：<请填写，参考下方分类列表>

## 分类列表（请选择最合适的一个）
ai, app, awk, blockchain, build, cicd, cloud, container, container-kube,
data-bin, data-csv-tsv, data-json-yml, data-line, data-text,
db, db-mysql, db-pg, db-sqlite,
editor, email, entertainment,
file-disk, file-manager, filesystem, finance, font,
iac, input-method,
journey,
lang, lang-js-ts, lang-perl-raku, lang-python, library, linter, log,
mac, markdown-html, misc, multimedia,
natural-language, network,
osman, other,
package-manager, programming,
reader,
scm, scm-git-service, scm-git-tool, scientific-computing, sdkman, security, shell, ssh,
temp, terminal, test,
virtualization,
wasm, web, web-apitool, web-browser, web-infrastructure, web-template

## 输出要求

请生成符合以下格式的 yml 内容：

```yaml
lang: <编程语言>
homepage: <主页URL>

desc:
  cn: <中文描述，一句话说明软件用途>
  en: <英文描述，一句话说明软件用途>

rule:
  darwin/brew:
    cmd: brew install <包名>
    reference: https://command-not-found.com/<包名>

  debian/apt:
    cmd: sudo apt-get install <包名>
    reference: https://command-not-found.com/<包名>

  arch/pacman:
    cmd: sudo pacman -S <包名>
    reference: https://command-not-found.com/<包名>
```

## 注意事项

1. `desc` 字段使用简洁描述，不要过度营销
2. `reference` 统一使用 https://command-not-found.com/<包名>
3. 如果该软件在某个系统没有官方包管理方式，可以省略该系统或使用通用安装方式如 /pip, /cargo, /go 等
4. 生成后请检查安装命令是否正确
```

---

## 简化版 Prompt

如果您只需要快速生成，可以直接问 AI：

```
请为 x-cmd install 仓库生成一个 yml 文件：
- 软件名：jq
- 主页：https://github.com/jqlang/jq
- 语言：Go
- 分类：data-json-yml

格式要求：
- lang, homepage, desc(cn/en), rule(os/manager: cmd + reference)
- reference 统一用 https://command-not-found.com/<包名>
```

---

## 验证生成结果

AI 生成后，请确认：
1. yml 语法正确
2. 安装命令准确
3. 放在正确的分类目录下
4. 参考 [YML 字段说明](./YML_SCHEMA.md) 进行最终检查
