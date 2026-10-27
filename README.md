# MA Codgent 官方站点

现代科技感的团队官网 / 内容矩阵入口，纯静态单文件，零依赖。

**线上地址（已上线）**
- 正式站：**`https://macodgent.pages.dev`** ← Cloudflare Pages，免费子域 + 自动 HTTPS + 全球 CDN
- 镜像站：`https://xieyj2026.github.io/MA-Codgent/` ← GitHub Pages 备份通道（同一份文件）

两个地址指向完全相同的内容，互为备份。以后想绑独立域名，内容一行不用改。

---

## 一、先改链接（唯一要动的地方）

打开 `index.html`，找到这段（在 `<script>` 里，很显眼）：

```js
const LINKS = {
  wechat: "Jian_Kayla",          // ← 联系微信号（已填）
  columns: [
    { ..., cta:"前往订阅", url:"#" },   // ← 把 # 换成专栏真实链接
    ...
  ],
  platforms: [
    { name:"CSDN", ..., url:"#" },       // ← 把 # 换成各平台主页链接
    ...
  ],
  contactSecond: "https://blog.csdn.net/2301_79425796"    // CSDN 主页（已填）
};
```

把每个 `url:"#"` 里的 `#` 换成真实网址即可。
- CSDN 主页示例：`https://blog.csdn.net/你的用户名`
- 邮箱：`mailto:name@example.com`
- 其它平台：直接贴对应主页/专栏地址

> 改完保存即生效，**不需要动其它任何代码**。微信号改 `wechat` 字段一处即可。

---

## 二、重新上线（改完内容后怎么推）

### 方式 A — Cloudflare Pages（正式站，推荐）
```bash
cd "/Users/xieyaojue/Documents/_MD CODE OPC/_51MDCODE产品和工程/_1 MDCODE官网"
./内容配置/部署到线上.sh
```
脚本会打包 `index.html` + `assets/` 并推到 Cloudflare Pages，约 10 秒完成。

### 方式 B — GitHub Pages（镜像站）
仓库 `XieYj2026/MA-Codgent`，网页上传（仓库页 → **Add file → Upload files**）→ Commit。
> 注意：GitHub 网页上传**不能覆盖同名文件**，先删旧文件再传新的。
> 上传后需在 Settings → Pages 选 Source = `Deploy from a branch` / `main` / `/ (root)`。

### 方式 C — 命令行（本机 mac 直推）
```bash
git init && git add . && git commit -m "MA Codgent 官网上线"
git branch -M main
git remote add origin https://github.com/XieYj2026/MA-Codgent.git
git push -u origin main
```

---

## 三、（可选）以后绑定自己的域名
等真有 B 端询盘、要印名片/写邮件签名时再买，站点内容一行不用改：
1. 在 Dynadot / NameSilo / Cloudflare Registrar 买域名（如 `macodgent.com`，支持支付宝、免实名）。
2. Cloudflare Pages 项目 → **Custom domains** → 添加域名 → 按提示在域名商处加 DNS 记录。
3. 免费 SSL 自动开，访问 `https://macodgent.com` 即官网。

---

## 文件说明
| 文件 | 作用 |
|---|---|
| `index.html` | 官网主页面（自包含，改 LINKS 即可）|
| `assets/poster.jpg` | 团队介绍海报（页面里展示 + 可下载，480KB）|
| `.nojekyll` | 关闭 GitHub 的 Jekyll 处理，避免静态资源被忽略 |
| `README.md` | 本说明 |

> 本地 `内容配置/`、`前端工程/`、`海报/` 为源文件 / 工作素材，已在 `.gitignore` 排除，不会进线上仓库。
