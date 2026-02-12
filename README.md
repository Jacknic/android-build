# Android APK Build

基于 GitHub Actions 的 Android APK 自动构建工具，支持灵活的仓库检出和自定义构建命令。

## ✨ 功能特性

- 🚀 **自动化构建**: 通过 GitHub Actions 自动构建 Android APK
- 🔧 **灵活配置**: 支持自定义仓库 URL、检出选项和构建命令
- 🎯 **智能 JDK 检测**: 根据 Gradle 版本自动选择合适的 JDK 版本
- 📦 **自动发布**: 构建完成后自动创建 GitHub Release 并上传 APK
- 📋 **构建报告**: 生成详细的构建信息报告

## 📖 使用方法

### 手动触发构建

1. 进入 GitHub 仓库的 **Actions** 标签页
2. 选择 **Android APK Build** 工作流
3. 点击 **Run workflow**
4. 填写以下参数：

| 参数 | 说明 | 必填 | 默认值 |
|------|------|------|--------|
| `repository_url` | Git 仓库 URL | 是 | - |
| `checkout_options` | git clone 参数（如 `-b branch_name --depth=1`） | 否 | `--depth=1` |
| `build_command` | 构建命令 | 是 | `bash gradlew asDebug` |
| `artifacts_pattern` | APK 文件路径模式 | 否 | `**/outputs/apk/**/*.apk` |

### 构建命令示例

```bash
# 构建 Debug 版本
bash gradlew assembleDebug

# 构建 Release 版本
bash gradlew assembleRelease

# 构建特定模块
bash gradlew :app:assembleDebug

# 构建所有变体
bash gradlew assemble
```

## 🔧 工作流说明

### JDK 版本自动检测

工作流会根据 Gradle 版本自动选择合适的 JDK 版本：

| Gradle 版本 | JDK 版本 |
|-------------|----------|
| 9.0+ | JDK 21 |
| 8.0 | JDK 17 |
| 7.0 | JDK 11 |
| 其他 | JDK 11 |

### 版本命名规则

生成的版本名称格式：`{日期时间}-{短提交哈希}`

示例：`20260212-143022-a1b2c3d`

### 构建产物

- APK 文件会自动上传到 GitHub Release
- Release 标签使用生成的版本名称
- 自动标记为 `latest` 版本
- 包含完整的构建报告

## 📁 项目结构

```
.
├── .github/
│   └── workflows/
│       └── build.yml          # GitHub Actions 工作流配置
├── .gitignore                 # Git 忽略文件配置
└── README.md                  # 项目说明文档
```

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来改进这个项目。

## 📄 许可证

本项目采用 MIT 许可证。
