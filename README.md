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


## 资料

站点规则、经验类笔记。

| 文档 | 内容 |
|---|---|
| [notes/seedbox-limits.md](notes/seedbox-limits.md) | 24 个 PT 站点的盒子（seedbox）刷流限制对照：黑白盒、上传倍率、单种限速、超速惩罚、RSS 频率、发种要求、VIP 价格、HR |
| [notes/auto-seedbox-pt.md](notes/auto-seedbox-pt.md) | Auto-Seedbox-PT 参考笔记：qB(v4/v5)+Vertex+FileBrowser 一键部署，Mode 1/2 调优、SSD/HDD 自适应（第三方，MIT） |


## 收录约定

发现新仓库时按这个规则处理，避免 `pt` 越堆越乱：

| 情况 | 做法 | 成本 |
|---|---|---|
| 只是想记住、以后可能要 | 写一条 `notes/<slug>.md`（照 `notes/_template.md`）+ 索引一行 | ~2 KB |
| 要长期用、版本要锁 | 加 **git submodule** 指向上游某个 commit | 几 KB |
| 上游可能消失 / 需要离线 | 只把**真正要跑的那几个脚本**拷进 `vendor/<slug>/`，附上 LICENSE | 几十 KB |
| 纯第三方大项目（>10 MB） | 只登记链接，不拷代码 | 0 |

原则：**不整仓拷贝**。第三方代码整仓进仓库会让 clone 变慢、许可证义务变复杂，而且上游一更新你这边就是过期副本。

## License

MIT



