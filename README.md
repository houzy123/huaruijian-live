# 华瑞健定向 - 赛事照片直播聚合页

微信公众号「华瑞健定向」的赛事照片直播聚合页面，对接拍立享云相册。

线上地址：https://houzy123.github.io/huaruijian-live/ （GitHub Pages）

## 快速开始

### 1. 添加新赛事

编辑 `index.html`，找到 `// 赛事数据配置区`（约第 200 行），在 `events` 数组中添加新赛事对象：

```javascript
{
    id: 9,                          // 唯一递增编号
    name: "2025年深圳定向公开赛",      // 赛事名称
    date: "2025-08-10",             // 排序用日期 (YYYY-MM-DD)
    dateDisplay: "2025年8月10日",    // 显示用日期
    location: "深圳市·笔架山公园",    // 地点
    cover: "照片封面图URL",           // 封面图（可先用 unsplash 占位）
    albumUrl: "https://live.pailixiang.com/xxxxxxx", // 拍立享相册链接
    photoCount: "1,200",            // 照片数量（结束后更新）
    status: "live",                 // "live"=正在直播, "past"=已结束
    year: "2025"                    // 年份（用于筛选）
}
```

### 2. 获取拍立享相册链接

1. 打开拍立享微信小程序 或登录 [拍立享官网](https://www.pailixiang.com/)
2. 进入"我创建的相册" → 找到对应活动
3. 点击「分享」→ 复制「云相册网址」
4. 将链接填入 `albumUrl` 字段

### 3. 更新封面图

封面图支持以下方式：
- **拍立享相册封面**：从拍立享后台复制相册封面图 URL
- **Unsplash 免费图**：`https://images.unsplash.com/photo-xxx?w=600&h=400&fit=crop`
- **自己上传**：将图片放入仓库，路径写为 `./images/xxx.jpg`

### 4. 部署到 GitHub Pages

修改后推送到 GitHub 仓库即可自动更新（约 1-2 分钟生效）：

```bash
git add index.html
git commit -m "添加 2025年深圳定向公开赛"
git push origin main
```

## 项目结构

```
.
├── index.html          # 主页面（赛事数据在此配置）
├── CNAME               # 自定义域名配置
├── README.md           # 本文件
└── .gitignore
```

## 公众号菜单配置

1. 登录 [微信公众平台](https://mp.weixin.qq.com/)
2. 内容与互动 → 自定义菜单
3. 一级菜单「照片直播」→ 子菜单「历届赛事」
4. 菜单内容选「跳转网页」→ 填入：`https://houzy123.github.io/huaruijian-live/`
5. 保存并发布

> 公众号必须完成微信认证才能添加外部链接。如未认证，可通过「自动回复」设置关键词（如"照片"）回复链接。

---

## 自定义域名配置（可选）

如需使用自己的域名（如 `huaruijian.live`）代替 `github.io`：

### 1. GitHub 仓库设置

1. 打开仓库 Settings → Pages
2. 在 **Custom domain** 填入你的域名，如 `huaruijian.live`
3. 勾选 **Enforce HTTPS**
4. 点击 Save

### 2. 域名 DNS 解析配置

在域名服务商（阿里云/腾讯云/GoDaddy 等）添加记录：

| 记录类型 | 主机记录 | 记录值 |
|---------|---------|--------|
| CNAME | `www` | `houzy123.github.io` |

如需根域名（不加 www），添加 A 记录指向 GitHub Pages IP：

| 记录类型 | 主机记录 | 记录值 |
|---------|---------|--------|
| A | `@` | 185.199.108.153 |
| A | `@` | 185.199.109.153 |
| A | `@` | 185.199.110.153 |
| A | `@` | 185.199.111.153 |

> DNS 生效需要几分钟到几小时。配置完成后回 GitHub Pages 设置页点击 **Check again**。

### 3. 仓库中的 CNAME 文件

仓库根目录的 `CNAME` 文件内容为自定义域名：
```
huaruijian.live
```

使用自定义域名后，GitHub 会自动将 `github.io` 地址重定向到自定义域名。

---

## 常见问题

### 1. 访问 `github.io` 地址被重定向到自定义域名且无法打开

**原因**：在 GitHub Pages 设置了自定义域名，但 DNS 没有正确配置，GitHub 缓存了重定向规则。

**解决**：
- 进入仓库 Settings → Pages → Custom domain
- 删除自定义域名 → 点击 **Remove**
- 清除浏览器缓存（Ctrl+Shift+Delete，勾选"缓存的图片和文件"）
- 等待 5-10 分钟后重新访问 `github.io` 地址
- 或使用无痕模式/换浏览器访问

### 2. 自定义域名显示 "DNS check unsuccessful"

**原因**：域名 DNS 记录未配置或尚未生效。

**解决**：
- 检查域名服务商的 DNS 解析记录是否正确（见上方配置表）
- 等待 DNS 生效（通常 10 分钟 - 48 小时）
- 点击 **Check again** 重新检测

### 3. push 代码后页面没有更新

**解决**：
- 确认 push 到了 `main` 分支
- 打开仓库的 Actions 页面，查看部署状态是否为绿色 ✓
- 等 1-2 分钟后强制刷新页面（Ctrl+Shift+R）

### 4. 微信内打开页面空白或排版错乱

**解决**：
- 确保使用的是 `https://` 开头的链接
- 检查网络连接，部分 Unsplash 封面图在微信内加载较慢，可替换为国内图床

---

## 技术说明

- 纯静态 HTML/CSS/JS，无需后端
- 适配手机端（微信内置浏览器优化）
- 支持按年份筛选赛事
- 点击卡片直接跳转到拍立享云相册
- 使用 GitHub Pages 免费托管，自带 HTTPS
