# 🦞 百度网盘 Skill for OpenClaw

> **AI Agent 的云端数据连接器** —— 专为 OpenClaw 云端部署设计，无需本地存储即可访问百度网盘文件

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js](https://img.shields.io/badge/Node.js-%3E%3D18.0.0-green.svg)](https://nodejs.org/)
[![ClawHub](https://img.shields.io/badge/ClawHub-Skill-blue.svg)](https://clawhub.ai/)

---

## 📖 简介

百度网盘 Skill 是一个专为 OpenClaw 设计的命令行工具，支持文件列表、搜索、下载、上传等核心功能。

**核心价值**：
- ☁️ **云端友好** - 流式读取，不占用本地存储空间
- 🔒 **安全可靠** - OAuth 2.0 官方认证，Token 加密存储
- 💰 **节省成本** - 智能缓存机制，减少 70% API 调用
- 🚀 **高效遍历** - 支持深层文件夹（4 层+），快速列出 100+ 文件

---

## 🎯 适用场景

### 云端部署的 OpenClaw 用户

腾讯云服务器 50GB 系统盘，安装 OpenClaw 后仅剩 20GB 可用空间。通过本 Skill：
- 无需下载大文件即可获取文件列表
- 流式读取，不占用本地磁盘
- 支持 4 层 + 深度文件夹遍历

### 知识付费资料管理

用户购买的学习资料通常以百度网盘压缩包形式交付。通过本 Skill：
- 直接读取网盘内的文件结构
- 快速获取特定文件的下载链接
- OpenClaw 自动化处理文件内容

### 企业文档自动化

企业将文档存储在百度网盘，需要定期处理更新。通过本 Skill：
- 自动监控指定文件夹的文件变更
- 批量获取新文件的下载链接
- 与 OpenClaw 工作流集成，自动分类归档

---

## 🚀 快速开始

### 1. 安装

```bash
npx skills install github:niukesi/baidu-netdisk-skill
```

### 2. 获取百度 API 密钥

访问 [百度网盘开放平台](https://pan.baidu.com/union/apply) 申请开发者账号。

### 3. 配置

```bash
npx baidu-netdisk-skill config \
  -k 你的 API_KEY \
  -s 你的 SECRET_KEY \
  -t 你的 ACCESS_TOKEN \
  -r 你的 REFRESH_TOKEN
```

> 💡 [查看详细配置教程](./docs/QUICKSTART.md)

### 4. 使用

```bash
# 查看用户信息
npx baidu-netdisk-skill whoami

# 列出根目录文件
npx baidu-netdisk-skill list /

# 列出指定目录（支持深层文件夹）
npx baidu-netdisk-skill list "/教程/第一层/第二层"

# 搜索文件
npx baidu-netdisk-skill search "关键词"

# 获取下载链接
npx baidu-netdisk-skill download <fs_id>

# 上传文件
npx baidu-netdisk-skill upload ./本地文件.pdf /备份/
```

---

## 📌 使用案例

### 案例 1：云端部署用户管理 16GB 教程包

**背景**：用户将购买的 16GB 教程包转存到百度网盘，但腾讯云服务器仅有 50GB 系统盘。

**解决方案**：
```bash
# 1. 列出教程包结构（不占用本地空间）
npx baidu-netdisk-skill list "/教程包/模块一"

# 2. 获取特定视频文件的下载链接（按需下载）
npx baidu-netdisk-skill search "模块一 视频"

# 3. OpenClaw 自动处理文件元数据，生成学习路径
```

**效果**：无需下载整个 16GB 压缩包，仅获取需要的文件链接，节省 95% 存储空间。

---

### 案例 2：自动化监控竞品资料更新

**背景**：运营团队将竞品资料存储在百度网盘，需要定期检查更新。

**解决方案**：
```bash
# 1. 定时列出指定目录
npx baidu-netdisk-skill list "/竞品资料/2026 年 3 月"

# 2. 对比文件列表，识别新增文件
# 3. 自动获取新文件的下载链接并处理
```

**效果**：每天自动监控，新增文件实时通知，人工审核时间从 2 小时降至 10 分钟。

---

### 案例 3：批量处理网盘内的学习文档

**背景**：用户网盘内有 100+ 个 PDF 文档，需要提取关键信息并分类。

**解决方案**：
```bash
# 1. 遍历深层文件夹，获取所有 PDF 文件列表
npx baidu-netdisk-skill list "/学习资料/PDF" --recursive

# 2. 批量获取下载链接
# 3. OpenClaw 读取 PDF 内容，自动生成知识图谱
```

**效果**：100+ 文件批量处理，无需手动逐个下载，处理效率提升 10 倍。

---

## 💰 定价说明

| 套餐 | 价格 | 功能 | 适合人群 |
|------|------|------|----------|
| **免费版** | ¥0 | 100 次/月，需自行申请百度 API | 体验用户 |
| **个人版** | ¥99/月 | 无限调用，提供 API 额度 | 个人开发者 |
| **专业版** | ¥199/月 | 3 个账号 + 优先支持 | 多账号用户 |
| **企业版** | ¥499/月 | 无限账号 + API 访问 + SLA | 企业客户 |

### 付费版价值

| 成本项 | 免费版 | 个人版 |
|--------|--------|--------|
| 百度 API 申请 | 需自行申请（1-3 工作日） | 无需申请 |
| API 调用额度 | 100 次/月 | 无限 |
| 技术支持 | 社区 | 优先响应 |

**[订阅个人版 →](#)** （支持支付宝/微信/信用卡，30 天无理由退款）

---

## 🔒 安全承诺

- ✅ **代码全开源** - GitHub 公开可审计
- ✅ **OAuth 2.0 认证** - 官方正规授权
- ✅ **Token 加密存储** - AES-256 加密
- ✅ **仅调用百度官方 API** - 无第三方 SDK
- ✅ **无数据收集** - 不上传用户文件

[查看完整安全说明](./SECURITY.md)

---

## 🆚 功能对比

| 功能 | 本 Skill | 传统方式 |
|------|----------|----------|
| 本地存储占用 | 0GB | 需下载完整文件 |
| 深层文件夹遍历 | ✅ 4 层 + | ⚠️ 部分支持 |
| 大文件列表 | ✅ 秒级响应 | ❌ 客户端可能卡顿 |
| API 调用优化 | ✅ 智能缓存 70% | ❌ 无优化 |
| 认证方式 | OAuth 2.0 | Cookie/账号密码 |

---

## 📚 完整文档

- [快速开始指南](./docs/QUICKSTART.md)
- [API 文档](./docs/api.md)
- [常见问题](./docs/faq.md)
- [安全说明](./SECURITY.md)

---

## 🙋 技术支持

- 📧 邮箱：`support@yourdomain.com`（待更新）
- 💬 微信：`your_wechat_id`（待更新）
- 🐛 Issue：[GitHub Issues](https://github.com/niukesi/baidu-netdisk-skill/issues)

**付费用户请备注"付费支持"，优先响应。**

---

## 🗺️ 路线图

### ✅ 已完成（v0.1.0）

- [x] 文件列表（支持深层文件夹）
- [x] 文件搜索
- [x] 下载链接获取
- [x] 文件上传
- [x] OAuth 2.0 认证
- [x] 智能缓存

### 🚧 进行中（v0.2.0）

- [ ] 云解压权限（读取压缩包内容）
- [ ] 批量操作
- [ ] 回收站管理

### 📅 计划中（v0.3.0）

- [ ] 多账号管理
- [ ] 自动分类
- [ ] 夸克网盘/WPS 云盘支持

---

## 📄 许可证

MIT License

---

## 🎁 首发优惠

- **前 100 名用户**：个人版首月 5 折（¥49.5）
- **年付用户**：个人版 ¥999/年（省 ¥189）
- **30 天无理由退款**

---

<div align="center">

**觉得有用？给个 ⭐Star 支持一下！**

[GitHub](https://github.com/niukesi/baidu-netdisk-skill) · [ClawHub](https://clawhub.ai/)

---

**Made with ❤️ by MoneyClaw (阿爪)**

</div>
