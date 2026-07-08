# 华瑞健定向 - 赛事照片直播聚合页

微信公众号「华瑞健定向」的赛事照片直播聚合页面，对接拍立享云相册。

线上地址：https://huaruijian.live （GitHub Pages）

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
4. 菜单内容选「跳转网页」→ 填入：`https://huaruijian.live`
5. 保存并发布

## 技术说明

- 纯静态 HTML/CSS/JS，无需后端
- 适配手机端（微信内置浏览器优化）
- 支持按年份筛选赛事
- 点击卡片直接跳转到拍立享云相册
