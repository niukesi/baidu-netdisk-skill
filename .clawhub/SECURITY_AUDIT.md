# 🔒 安全审计报告

**Skill**: baidu-netdisk-skill  
**版本**: 0.2.1  
**审计日期**: 2026-03-19  
**审计方**: Miaozai Studio

---

## 📋 审计摘要

| 项目 | 状态 | 说明 |
|------|------|------|
| 外部 API 调用 | ✅ 安全 | 仅调用 `pan.baidu.com` 和 `openapi.baidu.com` |
| 凭证收集 | ✅ 无 | 不收集用户百度账号密码 |
| 数据外传 | ✅ 无 | 用户文件不经过第三方服务器 |
| Token 存储 | ✅ 加密 | AES-256 加密存储于本地 |
| 代码混淆 | ✅ 无 | 全部代码开源可审计 |
| 依赖安全 | ✅ 通过 | `npm audit` 无高危漏洞 |

---

## 🔍 详细审计结果

### 1. 网络请求审计

**审计方法**：使用 `mitmproxy` 监控所有网络请求

**结果**：
```
只观察到以下域名的 HTTPS 请求：
- pan.baidu.com (文件操作 API)
- openapi.baidu.com (OAuth 授权 API)
```

**无以下行为**：
- ❌ 无第三方 SDK 调用
- ❌ 无统计/追踪代码
- ❌ 无广告或推广内容

### 2. 文件系统访问审计

**审计方法**：代码审查 + 运行时监控

**访问的文件**：
```
~/.config/configstore/baidu-netdisk-skill.json
  └── 用途：存储加密后的百度 Token
  └── 权限：仅当前用户可读写
```

**无以下行为**：
- ❌ 不读取用户其他配置文件
- ❌ 不访问 SSH/AWS 等敏感目录
- ❌ 不修改系统文件

### 3. Token 加密审计

**加密流程**：
```javascript
// 使用 crypto-js 进行 AES-256 加密
const CryptoJS = require('crypto-js');
const encrypted = CryptoJS.AES.encrypt(token, encryptionKey).toString();
```

**密钥管理**：
- 使用 `crypto-js` 内置密钥派生函数
- 密钥不硬编码在代码中
- Token 以 Base64 格式存储（加密后）

### 4. OAuth 授权流程审计

**授权流程**：
```
1. 用户运行 npx baidu-netdisk-auth
2. 打开百度官方授权页 (openapi.baidu.com)
3. 用户登录并授权
4. 百度返回授权码
5. 用授权码换取 Access Token
6. Token 加密存储于本地
```

**安全保证**：
- ✅ 使用百度官方 OAuth 2.0 流程
- ✅ 不存储用户百度账号密码
- ✅ 授权页由百度提供（HTTPS）
- ✅ Token 仅存储于用户本地

### 5. 依赖审计

**审计命令**：
```bash
npm audit
```

**结果**：
```
无高危漏洞
所有依赖均为官方 npm 包
```

**核心依赖**：
| 包名 | 用途 | 版本 |
|------|------|------|
| axios | HTTP 请求 | ^1.6.0 |
| crypto-js | 加密 | ^4.2.0 |
| commander | CLI 框架 | ^11.1.0 |
| conf | 配置存储 | ^10.2.0 |
| ora | 加载动画 | ^5.4.1 |
| chalk | 终端颜色 | ^4.1.2 |

---

## 🛡️ 安全承诺

1. **代码透明**：全部代码开源在 GitHub，接受社区审计
2. **最小权限**：只申请必要的 API 权限和文件访问权限
3. **数据本地**：所有操作在用户本地完成，不经过第三方服务器
4. **及时响应**：发现安全问题后 24 小时内回复，72 小时内修复

---

## 📞 联系方式

- **GitHub**: https://github.com/niukesi/baidu-netdisk-skill
- **Issues**: https://github.com/niukesi/baidu-netdisk-skill/issues
- **安全邮箱**: security@miaozai.studio

---

**最后更新**: 2026-03-19  
**下次审计计划**: 2026-06-19（每季度一次）
