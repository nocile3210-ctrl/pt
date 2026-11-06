# PT 工具箱

个人 PT 相关的工具与资料。**第三方项目的关键脚本都有本地快照，上游删库也不影响使用。**

| 分区 | 放什么 |
|---|---|
| [`tools/`](tools/) | 自己维护的工具（代码在本仓库里） |
| [`notes/`](notes/) | 第三方仓库笔记、站点规则等资料 |
| [`snapshots/`](snapshots/) | 关键源码快照 + 校验和，防上游删库/改协议 |

## 工具

| 工具 | 说明 | 形态 |
|---|---|---|
| [tracker-studio](tools/tracker-studio/) | Transmission / qBittorrent 的 tracker 批量管理：站点聚合、逐条 diff 预览、自动备份与一键回滚 | 本地 Web 应用（Python，零依赖）+ 篡改猴脚本 |

## 资料 / 笔记

| 文档 | 内容 |
|---|---|
| [notes/seedbox-limits.md](notes/seedbox-limits.md) | 24 个 PT 站点的盒子（seedbox）刷流限制对照：黑白盒、上传倍率、单种限速、超速惩罚、RSS 频率、发种要求、VIP 价格、HR |
| [notes/auto-seedbox-pt.md](notes/auto-seedbox-pt.md) | Auto-Seedbox-PT 参考笔记：qB(v4/v5)+Vertex+FileBrowser 一键部署，Mode 1/2 调优、SSD/HDD 自适应 |

新增笔记照 [notes/_template.md](notes/_template.md) 写。

## 快照（防上游删库）

| 快照 | 上游 | 版本 | 内容 |
|---|---|---|---|
| [snapshots/auto-seedbox-pt/](snapshots/auto-seedbox-pt/) | [yimouleng/Auto-Seedbox-PT](https://github.com/yimouleng/Auto-Seedbox-PT) | `8716b2d7f5d4` · 2026-09-08 | 部署主脚本、应用脚本、发种辅助脚本、LICENSE，附 SHA-256 |

每个快照目录里的 `SOURCE.md` 记录上游地址、commit、收录范围与校验和。

## 收录约定

发现新仓库时按这个规则处理：

| 情况 | 做法 | 成本 |
|---|---|---|
| 只是想记住、以后可能要 | 一条 `notes/<slug>.md`（照模板）+ 索引一行 | ~2 KB |
| 要长期用、版本要锁 | 加 **git submodule** 指向上游某个 commit | 几 KB |
| **上游可能删库 / 要能离线跑** | `snapshots/<slug>/` 只放**能独立跑的核心文件** + LICENSE + SOURCE.md | 几十~几百 KB |
| 纯第三方大项目（>10 MB） | 只登记链接，不拷代码 | 0 |

原则：**不整仓拷贝**。第三方代码整仓进仓库会让 clone 变慢、许可证义务变复杂，而且上游一更新你手里就是过期副本。

## 上游删库了还能用吗

| 东西 | 删库后 |
|---|---|
| `snapshots/` 里的脚本 | ✅ 能用，文件在你仓库里，`SOURCE.md` 有版本和校验和 |
| `notes/` 里的命令与说明 | ✅ 能用（文字描述不依赖上游） |
| 上游的完整仓库（二进制、备份包、git 历史） | ❌ 需要自己另存（体积大，不值当放仓库） |
| git submodule | ❌ 指向上游 commit，上游没了就 clone 不下来 |

所以关键项目的取舍是：**核心脚本进 snapshots/，大文件走本地或上游**。

## License

本仓库自带内容（`tools/`、`notes/`）为 MIT。`snapshots/` 下各第三方项目保留其原始许可，见各自目录内的 LICENSE。
