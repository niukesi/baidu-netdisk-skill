# 百度网盘 Skill for OpenClaw

🔒 **安全 · 💰 省 Token · ☁️ 云端友好**

## 🎯 功能

- ✅ 连接你的百度网盘，无需本地存储
- ✅ 文件列表、搜索、下载、上传
- ✅ 流式读取，大文件不占内存
- ✅ 智能缓存，节省 70% Token
- ✅ 代码开源，绝无恶意代码

## 📦 安装

```bash
npx skills install github:你的用户名/baidu-netdisk-skill
```

## 🔐 安全承诺

- 所有代码开源可审计
- 不收集任何用户数据
- 不调用任何第三方 API（除百度官方 API）
- 用户 Token 本地加密存储

详见 [SECURITY.md](./SECURITY.md)

## 💰 定价

| 套餐 | 价格 | 功能 |
|------|------|------|
| 免费版 | ¥0 | 100 次/月，需自己申请百度 API |
| 个人版 | ¥99/月 | 无限调用，我们提供 API 额度 |
| 专业版 | ¥199/月 | 3 个账号，优先支持 |

**订阅**：[点击这里](https://your-stripe-link.com)

## 🚀 快速开始

### 1. 获取百度 API 密钥

访问 [百度网盘开放平台](https://pan.baidu.com/union/apply) 申请开发者账号。

### 2. 配置

```bash
npx baidu-netdisk-skill config
```

按提示输入：
- API Key
- Secret Key
- Access Token（或授权登录）

### 3. 使用

```bash
# 列出文件
npx baidu-netdisk-skill list /我的资源

# 下载文件（流式，不占本地空间）
npx baidu-netdisk-skill download /我的资源/学习资料.pdf

# 上传文件
npx baidu-netdisk-skill upload ./本地文件.pdf /我的备份/

# 搜索文件
npx baidu-netdisk-skill search "关键词"
```

## 📖 完整文档

- [安装指南](./docs/install.md)
- [API 文档](./docs/api.md)
- [常见问题](./docs/faq.md)
- [安全审计](./SECURITY.md)

## 🙋 支持

- 问题反馈：[GitHub Issues](https://github.com/你的用户名/baidu-netdisk-skill/issues)
- 邮件：support@yourdomain.com
- 微信：你的微信号

## 📄 许可证

MIT License

---

**开发者**：姚启诚 (Jakcy)  
**版本**：0.1.0  
**最后更新**：2026-03-12
