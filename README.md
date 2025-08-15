# JSAPIscan 扫描工具

一个高性能的JavaScript API端点发现和扫描工具，专门用于从JavaScript文件中提取API接口信息并进行安全测试。

## 🚀 功能特性

- **🔍 智能API发现**: 自动从JavaScript文件中提取API端点路径
- **📱 多框架支持**: 支持Webpack、Vue、React等现代前端框架的JS文件解析
- **🚀 高性能扫描**: 多线程并发处理，支持自定义线程数
- **🛡️ 安全测试**: 内置未授权访问测试和POC验证功能（POC预计0.3开放）
- **📊 智能输出**: 自动生成CSV报告和详细日志（后续会出html报告）
- **🔧 灵活配置**: 支持批量URL扫描、自定义深度等
- **📁 自动管理**: 自动创建时间戳文件夹，结果分类存储

## 🛠️ 安装方法

 直接下载

从 [Releases](https://github.com/ruisika/jsapiscan/releases) 页面下载最新版本的预编译二进制文件。

## 📖 使用方法

### 基本用法

```bash
# 扫描单个URL
JSAPIscan.exe -u https://example.com

# 批量扫描URL文件
JSAPIscan.exe -f urls.txt

# 设置线程数和爬取深度
JSAPIscan.exe -u https://example.com -t 20 -d 5

```
<img width="1168" height="624" alt="image" src="https://github.com/user-attachments/assets/cd4dea00-8e39-4388-b8c7-27a8a66cd86d" />

### 高级用法

```bash
# 启用自动接口测试（-auto 是未授权访问检测 不加只会爬取）
JSAPIscan.exe -u https://example.com -auto

# 携带参数进行测试
JSAPIscan.exe -u https://example.com -auto -aparms

# 启用POC测试
JSAPIscan.exe -u https://example.com -auto -aparms -apoc

# 批量扫描并自动测试
JSAPIscan.exe -f urls.txt -auto -t 15 -d 4
```

## 🔧 命令行参数

| 参数 | 说明 | 默认值 | 示例 |
|------|------|--------|------|
| `-u` | 目标URL | - | `-u https://example.com` |
| `-f` | URL文件路径 | - | `-f urls.txt` |
| `-t` | 线程数 | 10 | `-t 20` |
| `-d` | 爬取深度 | 3 | `-d 5` |
| `-auto` | 启用自动接口测试 | false | `-auto` |
| `-aparms` | 携带参数测试 | false | `-aparms` |
| `-apoc` | 启用POC测试 | false | `-apoc` |
| `-h` | 显示帮助信息 | false | `-h` |

## 📁 输出结构

工具会在 `res/` 目录下自动创建时间戳文件夹，包含以下文件：

```
res/
└── 20250814_101335/
    ├── 1755137615.txt          # 主要扫描结果
    ├── api_scan_domain.csv     # API扫描CSV报告
    ├── findsometingzong.txt    # 发现内容汇总
    └── parms.txt              # 参数信息
```

## 📊 支持的框架

- **Webpack**: 自动解析chunk.js文件
- **Vue.js**: 识别Vue组件中的API调用
- **React**: 支持React应用的JS文件分析
- **通用JS**: 支持标准JavaScript文件解析

## 🚨 注意事项

1. **合法使用**: 请确保在获得授权的情况下使用本工具
2. **网络限制**: 建议设置合理的线程数和超时时间
3. **资源消耗**: 深度扫描会消耗较多网络和计算资源
4. **结果验证**: 扫描结果仅供参考，请进行人工验证

## 🤝 贡献指南

欢迎提交Issue和Pull Request！



## 📞 联系方式
![扫码_搜索联合传播样式-标准色版](https://github.com/user-attachments/assets/dc53e67f-3a17-4ef9-b8f6-48441dabbd7c)
- **GitHub**: [https://github.com/ruisika/jsapiscan](https://github.com/ruisika/jsapiscan)

---

**⚠️ 免责声明**: 本工具仅供安全研究和授权测试使用，使用者需承担相应的法律责任。
本工具/脚本/内容仅供合法的网络安全测试与技术研究使用，使用者在使用前必须遵守《中华人民共和国网络安全法》、《中华人民共和国刑法》、《计算机信息系统安全保护条例》等相关法律法规。

授权范围：仅限在取得相关系统或网站书面授权的情况下使用。

禁止用途：严禁将本工具/脚本/内容用于任何未经授权的渗透测试、攻击、入侵、数据窃取、破坏等违法行为。

法律责任：任何因不当使用本工具/脚本/内容而造成的法律后果及损失，由使用者自行承担，作者概不负责。

风险提示：在进行网络安全测试时，请确保对目标系统不造成中断、数据丢失或服务不可用等影响。

使用本工具/脚本/内容即视为您已阅读并同意以上免责声明。

## 250814更新
v0.27
添加图标计算hash
添加title显示
优化路径检测逻辑
