# PT 工具箱

个人 PT（Private Tracker）相关的脚本与工具合集。每个工具一个子目录，互不依赖。

| 工具 | 说明 | 形态 |
|---|---|---|
| [tracker-studio](tracker-studio/) | Transmission / qBittorrent 的 tracker 批量管理：站点聚合、逐条 diff 预览、自动备份与一键回滚 | 本地 Web 应用（Python，零依赖）+ 篡改猴脚本 |

## 关于 tracker-studio

换 PT 站域名或 passkey 时，几万个种子的 tracker 要一起改。这个工具把流程压成三步：

1. **看清单** —— 所有 tracker 按站点聚合，一眼看到哪个站有多少种子
2. **预览** —— 逐条列出「哪个种子、旧 URL → 新 URL」，确认后才执行
3. **可回滚** —— 执行前自动备份，出错一键撤销

两种形态任选：

- **篡改猴脚本**（零部署）：`tracker-studio/userscript/tracker-studio-lite.user.js`，注入 Transmission Web 页面，右下角 🧭 按钮
- **本地 Web 应用**：`python tracker-studio/tracker_studio.py --open`

详细文档见 [tracker-studio/README.md](tracker-studio/README.md)。

## License

MIT
