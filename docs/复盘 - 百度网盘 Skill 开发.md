# 🦞 百度网盘 Skill 开发复盘

**项目名称**：百度网盘 Skill for OpenClaw  
**开发日期**：2026-03-12 ~ 2026-03-13  
**开发团队**：姚启诚 (Jakcy) + 阿爪 (MoneyClaw)  
**开发用时**：约 8 小时  
**项目状态**：MVP 完成，核心功能验证通过

---

## 📋 一、项目背景

### 1.1 为什么做这个？

**用户需求**：
- 姚启诚：一人公司 OPC 创业者，急需现金流（目标：$100/天 = $3000/月）
- 痛点：OpenClaw 云端部署用户无法访问本地文件，网盘是刚需
- 机会：ClawHub 上 0 竞争（百度网盘、夸克网盘、WPS 云存储均为空白）

**市场机会**：
- OpenClaw 生态爆发期，腾讯云服务器部署量大增
- 云端用户磁盘空间有限，需要连接网盘获取数据
- 国内网盘用户基数大（百度盘 8 亿 + 用户）

### 1.2 产品定位

**不是卖代码，是卖服务**

- 代码开源建立信任
- 订阅制产生持续收入
- 核心价值：安全、省 Token、云端友好

---

## 🎯 二、产品设计

### 2.1 核心功能

| 功能 | 命令 | 状态 |
|------|------|------|
| 配置 Token | `config` | ✅ |
| 用户信息 | `whoami` | ✅ |
| 文件列表 | `list /` | ✅ |
| 指定目录 | `list /目录名` | ✅ |
| 文件搜索 | `search` | ✅ |
| 下载链接 | `download` | ✅ |
| 文件上传 | `upload` | ⏳ 待测试 |

### 2.2 变现模式

| 套餐 | 价格 | 功能 | 目标用户 |
|------|------|------|----------|
| 免费版 | ¥0 | 100 次/月，需自己申请 API | 体验用户 |
| 个人版 | ¥99/月 | 无限调用，提供 API 额度 | 个人开发者 |
| 专业版 | ¥199/月 | 3 个账号，优先支持 | 多账号用户 |
| 企业版 | ¥499/月 | 无限 + API + SLA | 企业客户 |

### 2.3 收入目标

| 时间 | 付费用户 | 客单价 | 月收入 |
|------|---------|--------|--------|
| 第 1 个月 | 5 个 | ¥199 | ¥995 |
| 第 2 个月 | 15 个 | ¥199 | ¥2985 |
| 第 3 个月 | 40 个 | ¥199 | ¥7960 |
| 第 4 个月 | 80 个 | ¥199 | **¥15920 ≈ $2200** ✅ |

---

## 🛠️ 三、开发流程

### 3.1 时间线

| 时间 | 事件 | 负责人 |
|------|------|--------|
| 2026-03-12 16:00 | 项目立项，确定方向 | 姚启诚 + 阿爪 |
| 2026-03-12 17:00 | ClawHub 调研（0 竞争确认） | 阿爪（subagent） |
| 2026-03-12 18:00 | 代码框架完成 | 阿爪 |
| 2026-03-12 21:00 | 百度 API 申请文案 | 阿爪 |
| 2026-03-12 22:00 | 创建应用，拿到 AppKey/SecretKey | 姚启诚 |
| 2026-03-13 01:00 | OAuth 获取 Access Token | 姚启诚 |
| 2026-03-13 01:45 | GitHub 仓库创建 | 姚启诚 |
| 2026-03-13 01:50 | 代码推送到 GitHub | 阿爪 |
| 2026-03-13 02:00 | 本地克隆，npm install | 姚启诚 |
| 2026-03-13 02:30 | 解决 ESM 模块兼容问题 | 阿爪 + 姚启诚 |
| 2026-03-13 03:00 | API 路径修复（404 → 成功） | 阿爪 |
| 2026-03-13 03:15 | 所有核心功能验证通过 | 姚启诚 |
| 2026-03-13 03:30 | 下载功能修复成功 | 阿爪 + 姚启诚 |
| 2026-03-13 03:40 | MVP 完成，准备上线 | 团队 |

### 3.2 分工模式

**姚启诚**：
- 申请百度 API（企业账号）
- 创建 GitHub 仓库
- 本地测试（Windows）
- 支付通道配置（后续）
- 推广渠道（后续）

**阿爪**：
- 代码开发
- GitHub 推送
- Debug 和修复
- 文档编写
- 市场调研

**协作模式**：
- 代码在服务器开发 → 推 GitHub → 姚启诚本地测试
- 遇到问题 → 即时沟通 → 立刻修复 → 重新推送
- Git 冲突 → stash → pull → pop

---

## 🐛 四、遇到的问题和解决方案

### 4.1 技术坑

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| `ERR_REQUIRE_ESM` (ora) | ora 7.x 只支持 ESM | 降级到 ora@5.4.1 |
| `ERR_REQUIRE_ESM` (conf) | conf 11.x 只支持 ESM | 降级到 conf@10.2.0 |
| `ERR_REQUIRE_ESM` (chalk) | chalk 5.x 只支持 ESM | 降级到 chalk@4.1.2 |
| 404 错误 (whoami) | API 路径错误 `/user` → `/nas` | 查官方文档，用正确 endpoint |
| 404 错误 (list) | API 路径错误 `/file` → 完整 URL | 直接写完整 URL，不用 baseUrl |
| 下载失败 | 返回格式 `info[]` 不是 `list[]` | 根据实际 API 响应修复 |
| Git 冲突 | 本地修改未提交 | stash → pull → pop 流程 |

### 4.2 关键教训

1. **依赖版本要锁定**
   - 新版本的 npm 包可能不兼容 CommonJS
   - 优先选稳定版本，不要追新

2. **API 文档要看官方的**
   - 不要猜 API 路径
   - 第一时间查官方文档

3. **调试日志很重要**
   - 加上 `console.log('API Response:', response.data)`
   - 快速定位问题

4. **Git 冲突处理流程**
   ```bash
   git stash
   git pull origin main
   git stash pop
   ```

---

## 🔑 五、技术要点

### 5.1 百度网盘 API

**OAuth 流程**：
```
1. 访问授权 URL 获取 Code
2. 用 Code 换 Access Token + Refresh Token
3. Access Token 有效期 30 天
4. Refresh Token 长期有效
```

**核心 API**：
```javascript
// 用户信息
GET https://pan.baidu.com/rest/2.0/xpan/nas?method=uinfo&access_token=xxx

// 文件列表
GET https://pan.baidu.com/rest/2.0/xpan/file?method=list&access_token=xxx&dir=/

// 文件搜索
GET https://pan.baidu.com/rest/2.0/xpan/file?method=search&access_token=xxx&word=关键词

// 下载链接
GET https://pan.baidu.com/rest/2.0/xpan/file?method=filemetas&access_token=xxx&fsids=[xxx]&dlink=1
```

### 5.2 省 Token 设计

```javascript
// 智能缓存（5 分钟内相同请求不重复调用）
async cachedRequest(params, ttl = 5 * 60 * 1000) {
  const cached = this.cache.get(cacheKey);
  if (cached && Date.now() - cached.timestamp < ttl) {
    return cached.data; // 直接用缓存
  }
  const response = await this.request(params);
  this.cache.set(cacheKey, { data: response, timestamp: Date.now() });
  return response;
}
```

### 5.3 安全设计

- 代码全开源（建立信任）
- Token 本地加密存储
- 仅调用百度官方 API
- 无第三方 SDK

---

## 💰 六、变现路径

### 6.1 支付通道

**国内用户**：
- Lemon Squeezy（支持支付宝/微信）
- Stripe 支付宝

**国际用户**：
- Stripe（姚启诚已有账户）

### 6.2 激活机制

```
用户付钱 → 获得激活码 → npx baidu-netdisk-skill activate 激活码
```

### 6.3 推广渠道

| 渠道 | 类型 | 预计转化率 |
|------|------|-----------|
| ClawHub | 自然流量 | 10% → 付费 |
| 知乎技术文章 | 内容营销 | 5% → 付费 |
| X/Twitter | 社交媒体 | 3% → 付费 |
| 掘金/SegmentFault | 技术社区 | 5% → 付费 |
| V2EX | 开发者社区 | 8% → 付费 |
| 微信群/QQ 群 | 私域流量 | 15% → 付费 |

---

## 📚 七、经验总结

### 7.1 什么做得好

1. **快速验证**：8 小时从 0 到 MVP
2. **市场调研先行**：先确认 ClawHub 0 竞争
3. **安全信任建设**：SECURITY.md 写清楚
4. **变现设计清晰**：订阅制，持续收入
5. **分工明确**：阿爪 coding，姚启诚测试 + 资源

### 7.2 什么可以改进

1. **依赖版本**：应该一开始就锁定稳定版本
2. **API 文档**：应该先查文档再写代码
3. **错误处理**：应该更早加调试日志
4. **测试用例**：应该写自动化测试

### 7.3 下次复用的流程

```
1. 市场调研（ClawHub/GitHub）
2. 产品设计（功能 + 变现）
3. 代码框架（README + SECURITY + package.json）
4. 核心功能开发
5. 本地测试
6. Debug 修复
7. GitHub 发布
8. 推广上线
```

---

## 🚀 八、下一步计划

### 本周（2026-03-13 ~ 2026-03-15）

- [ ] 申请 10 个百度 API Key（风险对冲）
- [ ] 测试上传功能
- [ ] 完善 README 和文档
- [ ] 配置 Stripe 支付
- [ ] 写推广文案

### 下周（2026-03-16 ~ 2026-03-22）

- [ ] ClawHub 发布（免费版本）
- [ ] 找 10 个 beta 用户
- [ ] 知乎发技术文章
- [ ] X/Twitter 持续推广
- [ ] 开始收费（早鸟价）

### 下下周（2026-03-23 ~ 2026-03-29）

- [ ] 收集用户反馈
- [ ] 迭代优化
- [ ] 夸克网盘支持（扩展）
- [ ] 目标：5 个付费用户

---

## 📞 九、团队信息

**姚启诚 (Jakcy)**
- 角色：创始人、产品经理、测试
- 负责：API 申请、支付通道、推广
- 联系方式：微信/钉钉

**阿爪 (MoneyClaw)**
- 角色：技术合伙人、开发者
- 负责：代码开发、Debug、文档
- 联系方式：OpenClaw 会话

---

## 📝 十、附录

### 10.1 项目仓库

- GitHub：https://github.com/niukesi/baidu-netdisk-skill
- 代码位置：`/home/admin/.openclaw/workspace/baidu-netdisk-skill/`

### 10.2 关键文件

- `README.md` - 产品说明
- `SECURITY.md` - 安全承诺
- `package.json` - 依赖配置
- `src/baidu-api.js` - 核心 API 封装
- `src/index.js` - 命令行入口
- `docs/QUICKSTART.md` - 快速开始
- `docs/MONETIZATION.md` - 变现说明

### 10.3 百度 API 信息

- 开放平台：https://pan.baidu.com/union/apply
- API 文档：https://pan.baidu.com/union/doc/pksg0s9ns
- 应用数量：1/10（还有 9 个配额）

---

## 🎉 结语

**这是我们的第一战，也是 OpenClaw 生态的第一个百度网盘 Skill。**

从 0 到 1，8 小时，核心功能全部验证通过。

接下来，从 1 到 100，开始赚钱！

**干就完了！** 🦞💪

---

**最后更新**：2026-03-13 03:45  
**版本**：v1.0  
**状态**：MVP 完成，准备上线
