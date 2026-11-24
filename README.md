# 🌌 StarLinkChat（星链终端）
基于 Kotlin + WebRTC + Jetpack Media3 + Node.js + MySQL + 阿里云 OSS 的全栈实时音视频通讯与个性化视频封面空间平台

一款独立全栈研发的移动端实时通讯与个性化空间社交应用，完整覆盖 **Android 原生客户端、WebRTC 音视频通话、Socket.IO 持久化 IM、Jetpack Media3 流媒体空间、Node.js 高可用后端与云端生产部署**。

> 📱 **真机体验包（Release APK）**：请点击右侧或此处前往 [Releases 发布页](https://api.zyw.ltd/downloads/StarLinkChat-v1.0.0.apk) 下载最新签名安装包 `StarLinkChat-v1.0.0.apk`（后端已部署于阿里云香港 HTTPS 节点，国内网络免代理直连）。

---

## 📸 实机运行截图 / App Screenshots

> 💡
<img width="1240" height="2772" alt="Screenshot_2026-11-22-14-08-48-15_1d4455926f8477d6c58e6787073ce808" src="https://github.com/user-attachments/assets/93031f29-67f9-4d4e-b5d1-d4b0078b9cf4" />
<img width="1240" height="2772" alt="IMG_20261122_141541" src="https://github.com/user-attachments/assets/2dd6bebc-045a-4b97-ad20-08b58f60fd73" />
<img width="1240" height="2772" alt="IMG_20261122_141602" src="https://github.com/user-attachments/assets/3eda13c3-2ce1-4c87-b31e-8c68408234ab" />
<img width="1240" height="2772" alt="IMG_20261122_141618" src="https://github.com/user-attachments/assets/4467e936-959b-4fc4-a192-c4b1a5f3d23b" />
<img width="1240" height="2772" alt="Screenshot_2026-11-22-14-13-27-82_1d4455926f8477d6c58e6787073ce808" src="https://github.com/user-attachments/assets/0879cdf5-47a0-40ff-a852-bb2f3bb3c799" />
<img width="1240" height="2772" alt="IMG_20261122_141514" src="https://github.com/user-attachments/assets/fb805c36-211a-4ac8-a2f8-feeb321f8169" />







## 🏗️ 系统架构 / System Architecture

```text
┌──────────────────────────────────────────────────────────────────────┐
│                     Android Client (Kotlin)                          │
│  ViewBinding · OkHttp · Socket.IO · WebRTC · Jetpack Media3 (Exo)    │
└──────────────┬───────────────────────────────────┬───────────────────┘
               │ HTTPS / WSS (api.zyw.ltd)         │ Presigned PUT (直传)
               ▼                                   ▼
┌──────────────────────────────┐     ┌─────────────────────────────────┐
│  Nginx (HTTPS / TLS / WS)    │     │     Aliyun OSS (深圳对象存储)     │
│  Certbot Auto-Renew          │     │   50MB 视频封面 / 15MB 空间音乐    │
└──────────────┬───────────────┘     └─────────────────────────────────┘
               │ Proxy (127.0.0.1:3000)
               ▼
┌──────────────────────────────┐     ┌─────────────────────────────────┐
│  Node.js + Express + Socket  │────▶│  MySQL 8.0 (qtaoi_db)           │
│  PM2 Daemon + JWT + 防刷风控   │     │  用户 / 好友 / 聊天 / 空间 / 限流  │
└──────────────┬───────────────┘     └─────────────────────────────────┘
               │
               ▼
┌──────────────────────────────┐
│  Aliyun DirectMail (SMTP/API)│
│  6位邮箱登录验证码下发          │
└──────────────────────────────┘
