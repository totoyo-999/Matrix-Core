<p align="center">
  <img src="https://img.shields.io/badge/Version-v4.0.0-blue?style=for-the-badge" alt="Version">
  <img src="https://img.shields.io/badge/Nodes-18-green?style=for-the-badge" alt="Nodes">
  <img src="https://img.shields.io/badge/Protocols-8-orange?style=for-the-badge" alt="Protocols">
  <img src="https://img.shields.io/badge/WARP-Cloudflare-6C3FC5?style=for-the-badge" alt="WARP">
  <img src="https://img.shields.io/badge/License-MIT-informational?style=for-the-badge" alt="License">
</p>

<h1 align="center">🦊 Matrix-Core</h1>

<p align="center">
  <strong>Sing-Box 18 节点多协议代理管理脚本</strong><br>
  18 节点 · 8 协议 · 直连 + WARP 双出口 · 全自动管理
</p>

---

## ✨ 特性

- 🔧 **一键部署** — 自动安装 sing-box、生成配置、注册 systemd 服务，一条命令搞定
- 🔀 **18 节点** — 9 个直连节点 + 9 个 WARP 节点，互为备份
- 🚀 **8 种协议** — 覆盖主流代理协议，性能与伪装兼顾
- ☁️ **Cloudflare WARP** — 官方 warp-cli 原生支持，流量经 Cloudflare 网络出口
- 📡 **订阅链接生成** — 兼容 v2rayN / sing-box，直接导入使用
- 🛠️ **可视化管理菜单** — 节点开关、测速、备份恢复、实时日志，全中文交互
- 🔒 **安全性** — 所有凭据运行时动态生成，脚本本身不包含任何硬编码密钥
- 🐧 **多系统兼容** — 支持 Debian / Ubuntu / CentOS / RHEL / Fedora / Arch / Alpine

---

## 📋 支持的协议

| 协议 | 类型 | 传输层 | TLS | 特点 |
|------|------|--------|-----|------|
| **VLESS-Reality** | 代理 | TCP | Reality | 基于 TLS 握手指纹伪装，抗审查能力极强，无证书依赖 |
| **VLESS-Reality (gRPC)** | 代理 | gRPC | Reality | 在 Reality 基础上使用 gRPC 传输，可伪装为正常 gRPC 流量 |
| **Trojan-Reality** | 代理 | TCP | Reality | 伪装为 HTTPS 流量，配合 Reality 证书无需域名 |
| **Hysteria2** | 代理 | UDP (QUIC) | 自签证书 | 基于 QUIC 协议，高速传输，弱网环境下表现优异 |
| **VMess-WS** | 代理 | WebSocket + TCP | 无 | 经典协议，通过 WebSocket 传输可套 CDN（Cloudflare） |
| **Shadowsocks 2022** | 代理 | TCP | 无 | SS 协议最新标准 (2022-blake3-aes-256-gcm) |
| **Shadowsocks** | 代理 | TCP | 无 | 经典 aes-256-gcm 加密，兼容性最广 |
| **TUIC v5** | 代理 | UDP (QUIC) | 自签证书 | 基于 QUIC 的新一代代理协议，原生多路复用 + BBR |

> 💡 **直连节点**流量直接从 VPS 出口出去；**WARP 节点**流量经 Cloudflare WARP 转发，出口 IP 为 Cloudflare IP。

---

## 📦 安装

### 快速安装（推荐）

```bash
wget -O sing-box-plus.sh https://raw.githubusercontent.com/totoyo-999/Matrix-Core/main/sing-box-plus.sh && chmod +x sing-box-plus.sh && ./sing-box-plus.sh
```

### 一键安装（curl）

```bash
bash <(curl -fsSL https://raw.githubusercontent.com/totoyo-999/Matrix-Core/main/sing-box-plus.sh)
```

### 系统要求

| 项目 | 最低要求 |
|------|---------|
| 系统 | Debian 9+ / Ubuntu 18.04+ / CentOS 7+ / RHEL 7+ / Fedora / Arch / Alpine |
| 架构 | x86_64 (amd64) / ARM64 / ARMv7 |
| 内存 | ≥ 256 MB |
| 磁盘 | ≥ 1 GB |
| 网络 | 需要能访问 GitHub 和 Cloudflare |

---

## 🎮 管理菜单

运行脚本后进入交互式管理菜单：

```
  1)  安装/部署（18 节点）
  2)  查看分享链接（IPv4）
  3)  重启服务
  4)  一键更换所有端口
  5)  一键开启 BBR
  6)  查看分享链接（IPv6）
  7)  节点开关管理        ← 自由启用/禁用任意协议
  8)  卸载
─────────────────────────
  9)  节点测速            ← TCP Ping 测试各节点延迟
  10) 订阅链接生成         ← 生成 Base64 订阅，v2rayN 可用
  11) 配置备份            ← 导出配置到 tar.gz
  12) 配置恢复            ← 从备份文件恢复
  13) 实时日志            ← 查看 sing-box 运行日志
─────────────────────────
  0)  退出
```

### 常用操作说明

**查看节点链接（导入客户端用）：**
```
运行脚本 → 选择 [2] → 复制对应协议的分享链接
```

**生成订阅地址（批量导入）：**
```
运行脚本 → 选择 [10] → 得到 Base64 订阅 URL
在 v2rayN 中：订阅 → 订阅设置 → 添加 → 粘贴 URL → 更新
```

**节点测速：**
```
运行脚本 → 选择 [9] → 自动 TCP Ping 所有启用节点
```

**备份 / 恢复：**
```
备份：运行脚本 → 选择 [11] → 自动导出到 /root/sing-box-backup-*.tar.gz
恢复：运行脚本 → 选择 [12] → 输入备份文件路径
```

---

## 📱 客户端推荐

| 平台 | 推荐客户端 | 支持协议 |
|------|-----------|---------|
| Windows | [v2rayN](https://github.com/2dust/v2rayN) | 全部 8 种 |
| macOS | [sing-box GUI](https://sing-box.sagernet.org/guide/installation/) | 全部 8 种 |
| Android | [sing-box (SFA)](https://sing-box.sagernet.org/guide/installation/) / [v2rayNG](https://github.com/2dust/v2rayNG) | 全部 8 种 |
| iOS | [sing-box (SFV)](https://sing-box.sagernet.org/guide/installation/) / [Shadowrocket](https://apps.apple.com/app/shadowrocket/id932747118) | 全部 8 种 |
| Linux | [sing-box CLI](https://sing-box.sagernet.org/guide/installation/) | 全部 8 种 |

---

## 🔧 配置文件位置

| 文件 | 路径 | 说明 |
|------|------|------|
| sing-box 配置 | `/opt/sing-box/config.json` | 主配置文件 |
| 数据目录 | `/opt/sing-box/data/` | 运行数据 |
| 凭据文件 | `/opt/sing-box/creds.env` | UUID、密钥等（自动生成） |
| 端口配置 | `/opt/sing-box/ports.env` | 各协议端口（自动生成） |
| WARP 配置 | `/opt/sing-box/warp.env` | WARP WireGuard 参数 |
| systemd 服务 | `/etc/systemd/system/sing-box.service` | 系统服务配置 |
| 订阅文件 | `/var/www/html/sub/singbox.txt` | Base64 格式订阅链接 |

---

## 🗂️ 项目结构

```
Matrix-Core/
├── sing-box-plus.sh    # 主脚本（18 节点：直连 9 + WARP 9）
└── README.md           # 项目说明
```

---

## 🔄 相关项目

| 项目 | 说明 | 链接 |
|------|------|------|
| **Totoyo999-SingBox** | 20 节点完整版（10 协议 + 节点图标 + Clash 订阅） | [GitHub](https://github.com/totoyo-999/Totoyo999-SingBox) |

---

## ⚠️ 注意事项

1. **Cloudflare WARP** 默认启用，需要 VPS 能访问 Cloudflare。如不需要可在「节点开关管理」中关闭
2. **Reality 协议**需要一个可访问的 TLS 站点（脚本默认使用 `www.microsoft.com`）作为伪装目标
3. **Hysteria2 / TUIC** 基于 UDP (QUIC)，请确保防火墙放行对应 UDP 端口
4. **端口随机生成**，首次部署时自动分配，如需自定义可在部署后通过「一键更换所有端口」修改
5. 建议部署后立即通过「配置备份」功能备份，方便后续迁移或恢复

---

## 📄 许可证

[MIT License](LICENSE)

---

<p align="center">
  Made with ❤️ by <a href="https://github.com/totoyo-999">totoyo-999</a>
</p>
