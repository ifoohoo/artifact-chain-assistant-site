# Artifact Chain Documentation Site

在线知识站（GitHub Pages）：[https://ifoohoo.github.io/artifact-chain-assistant-site/](https://ifoohoo.github.io/artifact-chain-assistant-site/)

本仓库承载 `artifact-graph` 与 `artifact-chain-assistant` 的独立静态公开文档站，集中提供产品概览、十分钟上手、制品图谱与四态对齐、批量工作流与方法注册表协同、命令行与退出码参考以及排障维护指南。直接浏览本站点无需安装任何命令行工具。

## 关联公开仓库

- [`ifoohoo/artifact-graph`](https://github.com/ifoohoo/artifact-graph) — Git 原生制品图扫描、关系校验、双向对齐与版本锁 CLI / Node.js 运行时
- [`ifoohoo/artifact-chain-assistant`](https://github.com/ifoohoo/artifact-chain-assistant) — 面向 Codex、Claude Code、Kimi Code、Qoder 与 Antigravity 的多宿主制品链协同插件

## 安装与最小只读示例

在线浏览可直接打开上方 GitHub Pages 地址。若需在本地模拟静态站点的子路径访问行为，可在克隆本仓库后于根目录启动只读静态服务：

```sh
python3 -m http.server 8000
```

页面、样式表、离线搜索索引与架构图全部采用相对路径与内容 SHA-256 指纹，不依赖第三方运行时 CDN 或外部字体，也不发起远端网络请求。

当对应精确版本已在公开源就绪且准备在业务仓库接入制品链时，可固定安装运行时与插件，并先执行只读帮助命令确认入口可用：

```sh
npm install --save-dev --save-exact artifact-graph@1.2.1
codex plugin add artifact-chain-assistant@artifact-skill-set
npx artifact-graph --help
```

<!-- release-skill:capability:safe-first-command -->
> **安全起点：** `npx artifact-graph --help` 与 `npx artifact-graph doctor --root .` 均为只读诊断命令，仅查看命令参数或核查本地配置健康度，不会修改项目文件、刷新版本锁或写入远端仓库。

<!-- release-skill:capability:external-write-boundary -->
> **外部写入边界：** 浏览静态站点或安装运行时不会触发任何远端写入。更新 `ifoohoo/artifact-chain-assistant-site` 的分支、标签、GitHub Release 或变更 GitHub Pages 设置，均须通过受控发布流水线并取得当次任务的明确授权。

## 常见故障诊断

- **离线搜索索引加载受限**：若直接通过本地 `file://` 协议双击打开 `index.html` 导致浏览器拦截 `assets/search-index.json` 读取，请改用上方 `python3 -m http.server 8000` 通过本地静态端口访问。
- **制品链门禁报错或锁漂移**：若运行 `validate`、`version-lock audit` 或 `alignment-audit` 时报告断链、陈旧锁或路径收容异常，请先执行 `npx artifact-graph doctor --root .` 定位原因，并参阅排障与维护手册：<https://ifoohoo.github.io/artifact-chain-assistant-site/troubleshooting.html>；下一步完整接入流程可参阅十分钟上手：<https://ifoohoo.github.io/artifact-chain-assistant-site/quickstart.html>。
- **发布准备或推送中断（`GATE_FAILED` / `PARTIAL`）**：维护者在源工作区联合发布本站点时，如遇 `GATE_FAILED` 请先按门禁阶段修复源 Markdown、重新渲染并刷新覆盖锁；如遇远端发布中断处于 `PARTIAL` 状态，应使用独立空 npm 缓存执行 `release-skill reconcile` 按既有证据恢复，再运行 `verify`，切勿强推覆盖远端分支或标签。

## 开源许可

Apache-2.0。详见 [LICENSE](LICENSE)。
