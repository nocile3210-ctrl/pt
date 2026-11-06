# Auto-Seedbox-PT (ASP) —— 参考笔记

> 上游：https://github.com/yimouleng/Auto-Seedbox-PT （MIT，Shell，⭐138）
> 本地参考副本：`<工作区>/refs/Auto-Seedbox-PT/`（未纳入本仓库，避免 60MB+ 体积）
> 仓库内快照：**[snapshots/auto-seedbox-pt/](../snapshots/auto-seedbox-pt/)** —— 核心脚本 + LICENSE + SHA-256，**上游删库也能用**
> 记录时间：2026-11-06

## 是什么

PT 专用 Seedbox 的一键部署脚本，面向 Debian 10+ / Ubuntu 20.04+，x86_64 与 arm64。除了装软件，重点在内核与 qB 参数的场景化调优。

## 装了什么

- **qBittorrent**（v4 / v5 双版本可选）
- **Vertex**（Docker，做种/统计前端，支持备份恢复与配置清洗）
- **FileBrowser + MediaInfo**（Docker + Nginx，网页内看媒体信息、视频智能截图，发种用）

## 两种调优模式

| 模式 | 适用 | 特点 |
|---|---|---|
| `-m 1` | 抢种刷流 | 强调连接建立效率与并发；内存 < 4GB 自动降级到 Mode 2 |
| `-m 2` | 长期保种 | 参数更平滑，持续上传、低波动 |

- 可选 `-a`：仅 Mode 1 生效的动态控制器，定时采样 MemAvailable / PSI，在 Boost / Normal / Guard 间切换，通过 qB WebAPI 动态调 `connection_speed`、`half-open`、per-torrent 连接、send buffer。
- SSD/HDD 自适应：按 Downloads 挂载盘的 `rotational` 识别盘型，分别选 I/O 与缓冲策略。
- systemd `MemoryHigh/MemoryMax` 约束 qB 进程；`-t` 可选 sysctl/网络/队列调优，且卸载可回滚。

## 快速开始

```bash
# Mode 1 抢种刷流（推荐可选 -a）
bash <(wget -qO- https://raw.githubusercontent.com/yimouleng/Auto-Seedbox-PT/main/auto_seedbox_pt.sh) \
  -u 用户名 -p 密码 -q 5 -m 1 -v -f -t -a
```

注意：统一密码要求 **≥ 12 位**。

## 与我这边工具的关系

- 本仓库的 [tracker-studio](../tracker-studio/) 管的是**已有种子库里的 tracker 批量替换**；
- ASP 管的是**从零部署/调优整台 Seedbox**。两者互补：先 ASP 把机器架起来，再用 tracker-studio 批量换站/换 passkey。

## 取舍记录

没有把代码拷进本仓库：上游 60 MB+（含 qB 二进制与备份包），且是 MIT 第三方项目，拷贝进来只会让 clone 变慢、还容易和上游不同步。需要源码时直接 clone 上游或看本地 `refs/` 副本。


## 快照说明

本仓库的 `snapshots/auto-seedbox-pt/` 保存了能独立运行的核心文件（部署主脚本、应用脚本、两个发种辅助 js、LICENSE、上游 README），并记录了 commit `8716b2d7f5d4` 与每个文件的 SHA-256。

没有收进快照的：`qBittorrent/` 目录与 `vt-backups.zip`（上百 MB 的二进制与备份包，需要时重新下载即可）。

换机器或上游消失时，直接 `sudo bash snapshots/auto-seedbox-pt/auto_seedbox_pt.sh <参数>` 即可，参数与原版一致。

