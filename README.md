# Renewlet 镜像仓库

[![同步状态](https://github.com/hopol/renewlet/actions/workflows/sync.yml/badge.svg)](https://github.com/hopol/renewlet/actions/workflows/sync.yml)
[![镜像发布](https://github.com/hopol/renewlet/actions/workflows/release.yml/badge.svg)](https://github.com/hopol/renewlet/actions/workflows/release.yml)
[![许可证](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## 简介

这是 [zhiyingzzhou/renewlet](https://github.com/zhiyingzzhou/renewlet) 的自动镜像仓库。

**Renewlet** 是一个自托管的订阅续费追踪器，支持时区感知提醒、10种通知渠道、预算和支出分析。

**本项目不做任何修改**，仅提供：
- 📦 **源码同步**：每5天自动备份上游源代码
- 🚀 **发布镜像**：自动镜像上游的二进制文件和 Docker 镜像
- 📝 **中文日志**：每个版本附带中文更新说明

## 为什么需要镜像？

GitHub 上的开源项目可能因为维护调整、作者归档等原因变得不可访问。本镜像仓库确保即使上游项目出现问题，源码和客户端仍然可用。

## 下载

前往 [Releases](https://github.com/hopol/renewlet/releases) 页面下载最新版本。

| 文件 | 说明 |
|------|------|
| `renewlet_{版本}_linux_amd64.tar.gz` | Linux x86_64 二进制文件 |
| `renewlet_{版本}_linux_arm64.tar.gz` | Linux ARM64 二进制文件 |
| `renewlet-docker-{版本}.zip` | Docker 镜像 |
| `checksums.txt` | 校验和文件 |

## 功能特性

- ✅ 订阅续费追踪
- ✅ 时区感知提醒
- ✅ 10种通知渠道支持
- ✅ 预算管理
- ✅ 支出分析
- ✅ 自托管部署

## 工作原理

### 源码同步（每5天）

```
上游仓库 (zhiyingzzhou/renewlet)
    ↓ git fetch
对比提交哈希
    ↓ 有变化
git archive 导出 → upstream/
    ↓
提交 & 推送 & 创建标签
```

### 发布镜像（每5天检查）

```
检查上游最新 Release
    ↓
是否已镜像？
    ├─ 是 → 跳过
    └─ 否 ↓
下载二进制文件和 Docker 镜像
    ↓
生成中文 Changelog + 原始日志
    ↓
创建镜像 Release（mirror-v{版本号}）
```

## 标签说明

| 标签格式 | 说明 | 示例 |
|----------|------|------|
| `mirror-v{版本}-{哈希}` | 源码同步标签 | `mirror-v0.2.95-abc1234` |
| `mirror-{版本}` | 发布镜像标签 | `mirror-0.2.95` |

## 项目结构

```
renewlet-mirror/
├── .github/
│   └── workflows/
│       ├── sync.yml           # 源码同步工作流（每5天）
│       └── release.yml        # 发布镜像工作流（每5天检查）
├── upstream/                  # 上游源码（运行时生成）
├── sync.sh                    # 本地同步脚本
├── README.md                  # 本文档
├── .gitignore
└── LICENSE
```

## 本地同步

```bash
git clone https://github.com/hopol/renewlet.git
cd renewlet
git remote add upstream https://github.com/zhiyingzzhou/renewlet.git
chmod +x sync.sh
./sync.sh
```

## 上游项目信息

- **项目名称**：Renewlet
- **上游仓库**：https://github.com/zhiyingzzhou/renewlet
- **技术栈**：TypeScript
- **上游许可证**：MIT
- **核心功能**：自托管的订阅续费追踪器
- **支持平台**：Linux (amd64/arm64)、Docker

## 许可证

本镜像仓库采用 [MIT 许可证](LICENSE)，与上游项目一致。

## 致谢

感谢 [zhiyingzzhou](https://github.com/zhiyingzzhou) 创建了优秀的 Renewlet 项目。
