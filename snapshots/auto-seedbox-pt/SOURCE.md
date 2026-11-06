# 快照来源

| 项 | 值 |
|---|---|
| 上游 | https://github.com/yimouleng/Auto-Seedbox-PT |
| 分支 | main |
| Commit | `8716b2d7f5d4` |
| 提交时间 | 2026-09-08 |
| 许可 | MIT（见同目录 LICENSE） |
| 快照时间 | 2026-11-06 |

## 为什么有这个目录

上游可能删库、改名或改协议。本目录保存**能独立跑起来的最小集合**，即使上游消失，部署逻辑仍然可用。

## 收录了什么

| 文件 | 大小 | SHA-256 |
|---|---|---|
| `auto_seedbox_pt.sh` | 91,775 | `55c87242f34af623bf8ea3f85dc2f30cd73771a8008c3a4fdbf7f741e1d64d6e` |
| `auto_seedbox_apps.sh` | 37,270 | `75f7d9aa833a1f838592d334b7b4afc6b9f2f012ca80cf90e8bcf9a48536132c` |
| `asp-mediainfo.js` | 10,653 | `07c41a1d7eb9971fa8d9111376d28a69073f9de47f838cda68986bb5b810b0ab` |
| `asp-screenshot.js` | 23,730 | `07caadf4d3b52e03df9d41638042e471b25a837680f7413995af2240d1bf8768` |
| `LICENSE` | 1,060 | `9aaa248bfaa71a48c1510b3d399e209fd39ba1d0d886c80393cd8a26c5c424c0` |
| `README.md`（上游原文） | 9,289 | `0b33e9be7f52bcda6a15260073660cd01e5fab1f13c6ef78e260fae4f612d894` |

## 没收录什么

- `qBittorrent/`、`vt-backups.zip` 等二进制与备份包（体积上百 MB，且能重新下载）
- 上游的 git 历史

## 怎么用

```bash
# 直接用快照脚本（把路径换成你 clone 下来的位置）
sudo bash snapshots/auto-seedbox-pt/auto_seedbox_pt.sh -u 用户 -m 1 -v -f -t -a
```

原脚本支持 `bash <(wget -qO- <url>)` 在线执行；用快照时改成 `sudo bash <本地路径>` 即可，参数完全一致。

## 校验

```bash
sha256sum auto_seedbox_pt.sh   # 应等于上表
```

## 升级

上游有更新时：`curl -sL https://api.github.com/repos/yimouleng/Auto-Seedbox-PT/commits/main | grep -m1 '"sha"'` 看新 commit，再重新抓取并更新本文件里的 SHA-256。
