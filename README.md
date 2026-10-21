# 云雀 3D 打印机 · 软件系统

> 基于开源 CoreXY 方案的自研 3D 打印机控制软件，覆盖手机端与电脑端，全程局域网部署。

[![项目状态](https://img.shields.io/badge/status-开发中-00E5C0)]()
[![技术栈](https://img.shields.io/badge/stack-React%20%2B%20FastAPI-4C8DFF)]()
[![网络](https://img.shields.io/badge/network-纯局域网-FFB020)]()

---

## 这是什么

把一台「必须守在旁边」的 3D 打印机，变成一台「可以在手机上看、在电脑上管、出问题会喊人」的智能设备。

| 能力 | 说明 |
|---|---|
| 远程监控 | 手机实时查看温度、进度、摄像头画面 |
| 远程控制 | 暂停、恢复、急停、控温、摇杆移动 |
| 文件闭环 | 手机上传 G-code，直接启动打印 |
| 故障告警 | 断料、超温、失联、视觉异常实时推送 |
| 视觉辅助 | OpenCV 检测炒面/首层异常，自动暂停 |
| 演示兜底 | 一键切换模拟数据，断网也能演示 |

---

## 系统架构

```
展示层  ─── 手机 H5 / 电脑 Electron / 红米2 触屏
   │      WebSocket (JSON-RPC) + HTTP
应用网关 ─── FastAPI（笔记本）：状态聚合 · 告警 · 视觉 · 存储
   │      Moonraker API
设备控制 ─── Klipper + Moonraker（笔记本主 / 红米2 备）
   │      USB 串口
执行层  ─── BIGTREETECH SKR 主板 + CoreXY 机械结构
```

---

## 快速开始

### 环境要求

- Node.js 18+
- Python 3.11+
- Klipper + Moonraker 已运行

### 前端

```bash
cd web
npm install
npm run dev        # 开发模式，访问 http://localhost:5173
npm run build      # 生产构建
```

### 后端网关

```bash
cd server
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

### 桌面端

```bash
cd electron
npm install
npm run dev        # 开发
npm run build      # 打包 exe
```

---

## 目录结构

```
.
├── docs/                  # 需求文档、开发计划、可视化页面
├── web/                   # 前端（手机 + 电脑共用）
├── server/                # FastAPI 网关
├── electron/              # Electron 桌面壳
├── screenshots/           # 截图统一存放
└── AGENTS.md              # 协作约定
```

---

## 文档

| 文档 | 说明 |
|---|---|
| [需求规格说明书](docs/需求规格说明书.md) | 完整功能定义、验收标准、技术方案 |
| [开发计划](docs/开发计划.md) | 六周排期与任务分解 |
| [可视化页面](docs/演示页面.html) | 架构图、功能矩阵、甘特图，答辩投屏用 |

---

## 技术栈

**前端**：React 18 · TypeScript · Vite · Tailwind CSS · ECharts · Three.js
**桌面**：Electron
**后端**：Python 3.11 · FastAPI · SQLite · OpenCV
**打印**：Klipper · Moonraker

---

## 设计原则

1. **纯内网**——不依赖任何外部云服务，断网不影响使用
2. **分层解耦**——展示层、网关层、控制层互不拖累
3. **安全优先**——急停全局可见、高风险操作二次确认、软限位保护
4. **可解释**——算法原理能向评委完整讲清楚

---

## 上游项目

本项目硬件基于 MakerWorld 开源模型「笨大鱼的 DIY 自制 3D 打印机 - 云雀 V1.06」二次开发，软件层自主实现。

---

## 许可证

软件部分：MIT License
硬件文档：遵循上游项目协议
