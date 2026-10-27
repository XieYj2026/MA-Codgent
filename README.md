# MA Codgent 官方站点

现代科技感的团队官网 / 内容矩阵入口，纯静态单文件，零依赖。

线上出口：**`https://macodgent.pages.dev`**（Cloudflare Pages 免费子域，自动 HTTPS + 全球 CDN，不带用户名，比 `github.io` 体面）。独立域名以后想加随时加，内容零返工。

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

## 二、上线（三步走）

### 1. 建仓库 + 授权
- 在 GitHub 新建公开仓库 **`MA-Codgent`**（Public，不要勾 README / .gitignore 模板）。
- 给推送用 PAT（`macodgent-push`）加 **`MA-Codgent` 仓库的 Contents: Read and write** 权限。

### 2. 推送站点文件到仓库根目录
需要进仓库的只有 5 个文件（其余源文件已被 `.gitignore` 排除，不进仓库、不影响线上）：
- `index.html`、`assets/`、`README.md`、`.nojekyll`、`.gitignore`

方式 A — 网页上传（最省事）：
仓库页 → **Add file → Upload files** → 拖入上述文件 → Commit。

方式 B — 命令行（本机 mac 直接推）：
```bash
git init
git add .
git commit -m "MA Codgent 官网上线"
git branch -M main
git remote add origin https://github.com/XieYj2026/MA-Codgent.git
git push -u origin main
```
> 注：WorkBuddy 沙箱环境直推 GitHub 会被代理拦截，改由维护者通过 GitHub Contents API 逐文件推送（绕过代理）。本机 mac 走上面命令正常。

### 3. 接 Cloudflare Pages（免费子域）
1. 注册 Cloudflare 账号（邮箱即可，无需实名）。
2. **Workers & Pages → Create → Pages → 连接 Git 仓库** → 选 `XieYj2026/MA-Codgent`。
3. 构建设置：**Framework preset = None（无构建）**，**Build command 留空**，**Output directory = `/`（根）**。
4. 部署完成后，Pages 自动分配子域 **`macodgent.pages.dev`** → 这就是官网地址。
5. 免费自动 HTTPS，全球 CDN，无需任何付费。

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
| `assets/poster.jpg` | 团队介绍海报（页面里展示 + 可下载，已压缩至 ~480KB）|
| `.nojekyll` | 关闭 GitHub 的 Jekyll 处理，避免静态资源被忽略 |
| `README.md` | 本说明 |

> 本地 `内容配置/`、`前端工程/`、`海报/` 为源文件 / 工作素材，已在 `.gitignore` 排除，不会进线上仓库。
