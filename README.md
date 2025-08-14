# JSAPIscan - JavaScript API 扫描工具

一个高性能的JavaScript API端点发现和扫描工具，专门用于从JavaScript文件中提取API接口信息并进行安全测试。

## 🚀 功能特性

- **🔍 智能API发现**: 自动从JavaScript文件中提取API端点路径
- **📱 多框架支持**: 支持Webpack、Vue、React等现代前端框架的JS文件解析
- **🚀 高性能扫描**: 多线程并发处理，支持自定义线程数
- **🛡️ 安全测试**: 内置未授权访问测试和POC验证功能
- **📊 智能输出**: 自动生成CSV报告和详细日志
- **🔧 灵活配置**: 支持批量URL扫描、自定义深度、代理设置等
- **📁 自动管理**: 自动创建时间戳文件夹，结果分类存储

## 📋 系统要求

- **操作系统**: Windows/Linux/macOS
- **Go版本**: 1.22.0+
- **内存**: 建议2GB+
- **网络**: 稳定的网络连接

## 🛠️ 安装方法

### 方法1: 从源码编译

```bash
# 克隆项目
git clone https://github.com/ruisika/jsapiscan.git
cd JSAPIscan

# 安装依赖
go mod tidy

# 编译项目
go build -o JSAPIscan.exe main.go  # Windows
go build -o JSAPIscan main.go      # Linux/macOS
```

### 方法2: 直接下载

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

# 指定输出文件
JSAPIscan.exe -u https://example.com -o results.txt
```

### 高级用法

```bash
# 启用自动接口测试（未授权访问检测）
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
| `-o` | 输出文件 | `res/timestamp/timestamp.txt` | `-o results.txt` |
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

## 🔍 扫描原理

1. **URL抓取**: 从目标网站抓取所有可访问的页面
2. **JS文件发现**: 自动识别和下载JavaScript文件
3. **API提取**: 使用正则表达式和解析器提取API端点
4. **智能分析**: 识别Webpack、Vue等框架的JS文件结构
5. **接口测试**: 对发现的API进行未授权访问测试
6. **结果生成**: 生成详细的CSV报告和日志文件

## 🏗️ 项目结构

```
JSAPIscan/
├── cmd/                    # 命令行参数处理
├── common/                 # 通用功能模块
├── config/                 # 配置管理
├── engine/                 # 扫描引擎
├── internal/               # 内部核心模块
│   ├── fetcher/           # 数据抓取器
│   ├── httpclient/        # HTTP客户端
│   ├── parser/            # JS解析器
│   ├── scheduler/         # 任务调度器
│   ├── storage/           # 数据存储
│   └── worker/            # 工作协程
├── report/                 # 报告生成
├── utils/                  # 工具函数
├── res/                    # 输出结果目录
├── main.go                 # 程序入口
└── README.md              # 项目说明
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

1. Fork 项目
2. 创建功能分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

## 📄 许可证

本项目采用 MIT 许可证 - 查看 [LICENSE](LICENSE) 文件了解详情

## 🙏 致谢

- 感谢所有贡献者的支持
- 特别感谢 [BTCSEC](https://github.com/ruisika) 团队

## 📞 联系方式

- **GitHub**: [https://github.com/ruisika/jsapiscan](https://github.com/ruisika/jsapiscan)
- **版本**: v0.26
- **作者**: BTCSEC Team

---

**⚠️ 免责声明**: 本工具仅供安全研究和授权测试使用，使用者需承担相应的法律责任。