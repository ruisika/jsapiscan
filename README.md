> 你们搞大模型的就是码奸，你们已经害死前端兄弟了，还要害死后端兄弟，测试兄弟，运维兄弟，害死网安兄弟，害死ic兄弟，最后害死自己害死全人类。

---

# 🛰️ JSAPIscan

![Go](https://img.shields.io/badge/Go-1.25%2B-00ADD8?logo=go&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)
![License](https://img.shields.io/badge/License-See%20LICENSE-blue)
![Build](https://img.shields.io/badge/Build-garble%20%7C%20go%20build-success)

一个 Go 语言开发的 JS 文件发现与接口扫描工具 🔎 —— A high-performance JavaScript endpoint discovery & unauthorized-access testing tool written in Go.

**🌐 语言 / Language:** [🇨🇳 中文](#-中文文档) · [🇬🇧 English](#-english-docs)

---

## 🇨🇳 中文文档

### 📖 简介

一个 Go 语言开发的 JS 文件发现和接口扫描工具，专门用于从 JavaScript 文件中提取 API 接口信息并进行安全测试。

- 🐛 发现 bug 可以提交 Issues，**一周内会解决**。
- 🤝 欢迎大家对比评测。如果爬取的 JS 文件或者路径没别的工具爬的多，随时与我联系，我看看这么个事。
- 🐢 说"快速"是假的 —— 涉及到太多 JS 文件的时候也会很慢。
- 🐼 规则大部分来自**熊猫头**，所以一般熊猫头能看到的该工具也没问题；如果熊猫头能行我的不行，求求你联系我，我看看这么个事。
- 🧧 如果发现这种形式的 JS 无法进行正确匹配，联系我会有**红包奖励**，感谢！

### ✨ 功能特性

- 🕸️ 深度 JS 爬取，自动解析 Webpack chunk / RequireJS 模块
- 🔓 API 接口自动提取 + 未授权访问测试（GET 405 自动 POST 重试）
- 🕵️ 敏感信息识别（身份证 / 手机号 / 邮箱 / JWT / AK-SK 等）
- 🧭 Vue Router 路径提取
- 🧩 前端组件漏洞识别
- 🧠 Headless 无头浏览器模式（Rod），面向重 JS 单页应用
- 🌐 外链扫描（CDN / 跨域 JS）
- 📝 多格式输出：TXT / HTML / CSV

### 🚀 快速开始

> 需要 Go **1.25+**。

```bash
# 标准构建
go build -o JSAPIscan.exe main.go         # Windows
go build -o JSAPIscan main.go             # Linux / macOS

# 多平台 + 混淆构建（需要 garble）
build.bat
```

```bash
# 单 URL 扫描
JSAPIscan.exe -u https://example.com

# 批量扫描
JSAPIscan.exe -f urls.txt

# 无头浏览器模式（适合重 JS 页面）
JSAPIscan.exe -u https://example.com -gorog
```

### 🛠️ 参数说明

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `-u` | | 目标 URL（逗号分隔支持多个） |
| `-f` | | 批量 URL 文件路径 |
| `-t` | 5 | 线程数（使用 `-u` 时强制为 1） |
| `-d` | 8 | 爬取深度 |
| `-time` | 10 | 单次请求超时（秒） |
| `-maxreq` | 4000 | 单个 URL 最多 JS 请求数 |
| `-maxhtml` | 40 | 单个 URL 最多 HTML 请求数 |
| `-maxapi` | 3000 | 单目标最多 API 测试数量（0 不限制） |
| `-header` | | 自定义请求头 `"Key:Value\r\nKey2:Value2"` |
| `-p` | | 代理 `http://127.0.0.1:8080` |
| `-pa` | false | 只对接口未授权测试使用代理 |
| `-tlsverify` | false | 校验服务器 TLS 证书（扫内网自签证书保持关闭） |
| `-gorog` | false | 开启无头浏览器模式 |
| `-savejs` | false | 保存爬取到的 JS 源文件到 `res/js/` |
| `-sc` | | 过滤显示的状态码，逗号分割 |
| `-gjca` | | 追加自定义敏感关键字，逗号分割 |
| `-gjc` | | 仅使用自定义关键字（替换默认） |
| `-aget` | false | 接口测试只使用 GET |
| `-basejspath` | | 自定义 JS 路径前缀（生成带/不带前缀两次请求） |
| `-baseapipath` | | 自定义 API 路径前缀（生成带/不带前缀两次请求） |
| `-extlink` | false | 开启外链扫描 |
| `-extlinksuffix` | `.js,.html,.htm` | 外链扫描后缀，逗号分割 |
| `-extlinkdepth` | 1 | 外链扫描深度 |
| `-domainblock` | | 域名黑名单，逗号分割（默认含 github/google/bing 等） |
| `-o` | txt | 输出格式 `txt` / `html` |
| `-K` | false | 只打印关键文件 |
| `-Ineedparms` | false | 开启参数提取并写入 `Params.txt` |

### 📂 输出结构

结果保存在 `res/<timestamp>/`：

```
res/20260212_150405/
├── 🔥 敏感详细.txt          # 敏感信息汇总
├── 📊 api_scan_*.csv        # 接口测试结果（状态 / 长度 / Body / 耗时）
├── 🗺️ js敏感信息对应.txt    # JS 文件 → 敏感信息 映射
├── 🗂️ 特殊文件路径.txt      # 特殊 / 敏感文件路径
├── ⬇️ 文件下载.txt          # 可下载文件（Content-Disposition: attachment）
├── 🧩 组件漏洞.txt          # 组件漏洞
├── 🛑 漏洞.txt              # 通用漏洞
├── 🧭 Vue路径信息.txt       # Vue 路由路径
├── 🕵️ 敏感内容.txt          # 敏感内容匹配
├── 🔑 关键词匹配.txt        # 自定义关键字命中
├── 📝 Params.txt            # 提取参数（-Ineedparms）
└── 📁 js/                   # 保存的 JS 源文件（-savejs）
```

### 🧪 进阶用法

**自定义请求头 / 认证**

```bash
# Bearer Token
JSAPIscan.exe -u https://example.com -header "Authorization:Bearer eyJhbGci..."

# 多个头
JSAPIscan.exe -u https://example.com -header "Authorization:Bearer token\r\nX-Custom:value"
```

**代理**

```bash
# 全局代理
JSAPIscan.exe -u https://example.com -p http://127.0.0.1:8080

# 只对接口测试阶段走代理（爬取阶段直连）
JSAPIscan.exe -u https://example.com -p http://127.0.0.1:8080 -pa
```

**无头浏览器**

```bash
JSAPIscan.exe -u https://example.com -gorog
```

**外链扫描**

```bash
JSAPIscan.exe -u https://example.com -extlink -extlinksuffix ".js,.mjs" -extlinkdepth 2
```

**自定义敏感关键字**

```bash
# 追加
JSAPIscan.exe -u https://example.com -gjca "password,secret_key,admin"

# 仅使用（替换默认）
JSAPIscan.exe -u https://example.com -gjc "internal_api,debug_mode"
```

### 📦 作为 Go 库使用

作为 SDK 调用请看 👉 [README_SDK.md](README_SDK.md)。

### 🐛 反馈

- Issues：提交后 **一周内** 响应
- 红包悬赏：遇到匹配不到的 JS 形态，欢迎联系作者 🎁

---

## 🇬🇧 English Docs

### 📖 About

A JavaScript endpoint discovery and interface-scanning tool written in Go, focused on extracting API routes from JS files and performing unauthorized-access testing.

- 🐛 File issues if you hit bugs — **resolved within a week**.
- 🤝 Benchmarks welcome. If another tool crawls more JS / paths than this one, reach out and I'll take a look.
- 🐢 "Fast" is aspirational — when a target ships lots of JS, it can still be slow.
- 🐼 Rules are largely inspired by **PandaHead (熊猫头)**; anything PandaHead detects, this should too. If PandaHead finds something this one misses, please tell me.
- 🧧 If you have a JS pattern that can't be matched, contact me — **red-packet reward** included.

### ✨ Features

- 🕸️ Deep JS crawling with Webpack chunk & RequireJS module parsing
- 🔓 API extraction + unauthorized-access tests (auto POST retry on GET 405)
- 🕵️ Sensitive data detection (ID cards, phones, emails, JWT, access keys)
- 🧭 Vue router path extraction
- 🧩 Frontend component vulnerability detection
- 🧠 Headless Chrome mode (Rod) for JS-heavy SPAs
- 🌐 External-link scanning (CDN / cross-origin JS)
- 📝 Multi-format output: TXT / HTML / CSV

### 🚀 Quick Start

> Requires Go **1.25+**.

```bash
# Standard build
go build -o JSAPIscan.exe main.go         # Windows
go build -o JSAPIscan main.go             # Linux / macOS

# Multi-platform + obfuscated build (requires garble)
build.bat
```

```bash
# Single URL
JSAPIscan.exe -u https://example.com

# Batch from file
JSAPIscan.exe -f urls.txt

# Headless browser
JSAPIscan.exe -u https://example.com -gorog
```

### 🛠️ Parameters

| Flag | Default | Description |
|------|---------|-------------|
| `-u` | | Target URL (comma-separated for multiple) |
| `-f` | | Batch URL file path |
| `-t` | 5 | Thread count (forced to 1 when `-u` is used) |
| `-d` | 8 | Crawl depth |
| `-time` | 10 | Per-request timeout (seconds) |
| `-maxreq` | 4000 | Max JS requests per URL |
| `-maxhtml` | 40 | Max HTML requests per URL |
| `-maxapi` | 3000 | Max API tests per target (0 = unlimited) |
| `-header` | | Custom headers: `"Key:Value\r\nKey2:Value2"` |
| `-p` | | Proxy: `http://127.0.0.1:8080` |
| `-pa` | false | Use proxy only for API testing |
| `-tlsverify` | false | Verify server TLS certs (keep off for self-signed internal targets) |
| `-gorog` | false | Headless browser mode |
| `-savejs` | false | Save crawled JS files to `res/js/` |
| `-sc` | | Filter status codes, comma-separated |
| `-gjca` | | Append custom sensitive keywords, comma-separated |
| `-gjc` | | Use only custom keywords (replaces defaults) |
| `-aget` | false | API testing uses GET only |
| `-basejspath` | | Custom JS path prefix (issues both prefixed & unprefixed requests) |
| `-baseapipath` | | Custom API path prefix (issues both prefixed & unprefixed requests) |
| `-extlink` | false | Enable external-link scanning |
| `-extlinksuffix` | `.js,.html,.htm` | External-link suffixes, comma-separated |
| `-extlinkdepth` | 1 | External-link scan depth |
| `-domainblock` | | Domain blocklist, comma-separated (default includes github/google/bing etc.) |
| `-o` | txt | Output format (`txt` or `html`) |
| `-K` | false | Print key files only |
| `-Ineedparms` | false | Extract parameters into `Params.txt` |

### 📂 Output Layout

Results are written to `res/<timestamp>/`:

```
res/20260212_150405/
├── 🔥 敏感详细.txt          # Sensitive-findings summary
├── 📊 api_scan_*.csv        # API test results (status / length / body / duration)
├── 🗺️ js敏感信息对应.txt    # JS file → sensitive info mapping
├── 🗂️ 特殊文件路径.txt      # Special / sensitive file paths
├── ⬇️ 文件下载.txt          # Downloadables (Content-Disposition: attachment)
├── 🧩 组件漏洞.txt          # Component vulnerabilities
├── 🛑 漏洞.txt              # General vulnerabilities
├── 🧭 Vue路径信息.txt       # Vue router paths
├── 🕵️ 敏感内容.txt          # Sensitive-content hits
├── 🔑 关键词匹配.txt        # Custom-keyword hits
├── 📝 Params.txt            # Extracted params (-Ineedparms)
└── 📁 js/                   # Saved JS sources (-savejs)
```

### 🧪 Advanced Usage

**Custom headers / auth**

```bash
# Bearer token
JSAPIscan.exe -u https://example.com -header "Authorization:Bearer eyJhbGci..."

# Multiple headers
JSAPIscan.exe -u https://example.com -header "Authorization:Bearer token\r\nX-Custom:value"
```

**Proxy**

```bash
# Global proxy
JSAPIscan.exe -u https://example.com -p http://127.0.0.1:8080

# Proxy only for the API-testing phase
JSAPIscan.exe -u https://example.com -p http://127.0.0.1:8080 -pa
```

**Headless browser**

```bash
JSAPIscan.exe -u https://example.com -gorog
```

**External-link scanning**

```bash
JSAPIscan.exe -u https://example.com -extlink -extlinksuffix ".js,.mjs" -extlinkdepth 2
```

**Custom sensitive keywords**

```bash
# Append
JSAPIscan.exe -u https://example.com -gjca "password,secret_key,admin"

# Replace defaults
JSAPIscan.exe -u https://example.com -gjc "internal_api,debug_mode"
```

### 📦 Use as a Go Library

See 👉 [README_SDK.md](README_SDK.md) for SDK-style API usage.

### 🐛 Feedback

- Issues are triaged **within a week**.
- Got a JS pattern that slips past detection? Ping the author — 🎁 red-packet reward for reproducers.

---

## 📄 License

See [LICENSE](LICENSE).
