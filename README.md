# 🧭 导航站

把你浏览器里几万个收藏夹，变成一个漂亮、好搜、装得下的起始页。

🌐 在线访问：**[leilaomi.sld.tw](https://leilaomi.sld.tw)**

---

## ✨ 功能

### 📦 装得下
- **IndexedDB 存储** — 轻松装下 30,000+ 书签，不再卡 `localStorage` 5MB 配额
- 大数据走 IndexedDB（书签本体），小数据走 localStorage（主题/点击统计），各取所长
- 旧用户首次打开自动从 localStorage 迁移到 IndexedDB，无感

### 🗂 找得到
- **完整保留浏览器的文件夹结构** — 顶部 chips 切换分类
- 1700+ 分类也能用：超过 20 个时点 **「更多」**，弹出搜索式分类选择器
- **跨分类搜索**：搜索框（带防抖 180ms）+ <kbd>Ctrl/⌘+K</kbd> 全屏 Spotlight，匹配名称和 URL
- **⭐ 常用区** — 自动按点击次数推荐 Top 12，越用越懂你

### 🎨 看着舒服
- 卡片悬浮 + 渐变高光 + 主色描边动效
- **彩色字母兜底** — favicon 加载失败时，按名字 hash 出独立色（再也不是一墙紫色）
- **3 源 favicon 轮询** — DuckDuckGo → Google → Yandex，最大化命中率
- **三态主题** — 跟随系统 / 浅色 / 深色，切换自动记忆
- **紧凑/宽松** 两档密度，30000 个书签时切紧凑模式视野翻倍
- 顶部 hero 区：大时钟 + 中文问候 + 日期 + 统计

### ⌨️ 用得快
| 快捷键 | 作用 |
|--------|------|
| <kbd>/</kbd> | 聚焦搜索框 |
| <kbd>Ctrl/⌘+K</kbd> | 打开全屏 Spotlight |
| <kbd>Esc</kbd> | 关闭弹层 / 清空搜索 |
| 拖文件入页 | 直接导入 |

### 📱 装得起来
- **PWA** — 浏览器「添加到主屏幕」当 App 用
- **离线访问** — Service Worker 缓存核心资源
- 移动端响应式布局，dock 自动落到底部居中

### 🔐 私密
- **所有数据本地存储**，**不上传任何服务器**
- 一键导出 JSON 备份 / 跨设备迁移
- 一键清空所有数据

---

## 🚀 使用

### 第一次用
1. 浏览器导出书签：
   - Chrome / Edge：`⋮` → 收藏夹 → 收藏夹管理器 → `⋮` → 导出书签
   - Firefox：`☰` → 书签 → 管理书签 → 导入和备份 → 导出书签到 HTML
   - Safari：文件 → 导出书签
2. 打开 [leilaomi.sld.tw](https://leilaomi.sld.tw)
3. **把文件拖进页面**（或点 📂 选择）— 完成！

### 备份与迁移
- 点 ↓ 按钮导出 JSON 文件
- 在新设备 / 新浏览器中拖入这个 JSON 即可恢复

---

## 🧩 顶部 dock 按钮

| 按钮 | 功能 |
|------|------|
| ▦ | 紧凑 / 宽松模式切换 |
| ◐ | 主题循环（跟随系统 → 浅色 → 深色） |
| ↓ | 导出 JSON 备份 |
| ⌫ | 清空所有数据（含确认） |

---

## 🛠 技术栈

- **单文件 HTML/CSS/JS**，无构建、无依赖、无后端
- **IndexedDB** 存储书签数据，**localStorage** 存元数据
- 标准 [Netscape 书签格式](https://msdn.microsoft.com/en-us/library/aa753582.aspx) 解析，兼容主流浏览器
- 渐进式渲染：每批 100 张卡片，滚动到底自动加载
- favicon 3 源容错：DuckDuckGo + Google + Yandex

## 📁 项目结构

```
.
├── index.html       # 主页面（30KB 单文件）
├── manifest.json    # PWA 配置
├── sw.js            # Service Worker（离线缓存）
├── icon.svg         # 应用图标
├── CNAME            # GitHub Pages 自定义域名
├── LICENSE          # MIT
└── README.md
```

## 📦 部署

仓库内容直接传到任何静态托管即可：

- **GitHub Pages**（当前部署方式）：push 到 `main` 自动部署
- **Cloudflare Pages / Vercel / Netlify**：一键导入仓库
- **自己的服务器 / Nginx**：把 5 个核心文件丢到 web 根目录即可

---

## 🎨 自定义

打开 `index.html`，搜索 `:root` 改主题色：

```css
:root{
  --accent: #4a90c4;       /* 主色 */
  --accent-bg: #e8f1f9;    /* 主色背景 */
  --radius: 14px;          /* 圆角 */
}
html.dark{
  --accent: #7ab8e0;       /* 暗色模式主色 */
}
```

修改 `manifest.json` 改 PWA 名称和图标颜色。

---

## ❓ 常见问题

**Q: 数据会丢吗？**  
A: 数据存在你浏览器的本地数据库（IndexedDB），清浏览器数据会丢。建议定期点 ↓ 导出 JSON 备份。

**Q: 为什么有些 favicon 是字母？**  
A: 该网站没有图标，或者 DuckDuckGo / Google / Yandex 三个源都拿不到。这时显示首字母兜底（按名字着色，每个站颜色独立）。

**Q: 怎么换设备继续用？**  
A: 老设备点 ↓ 导出 JSON，在新设备打开网站，把 JSON 拖进去即可。

**Q: 能不能从书签里删条？**  
A: 暂时不能（保持简洁）。删了直接在浏览器里删，重新导出导入即可。

---

## 📜 License

MIT © LeilaoMi
