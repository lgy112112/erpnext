# Communication 模块（通信媒介）

## 概述
定义通信媒介和时间段，用于电话集成和客户沟通渠道管理。

## 规模
- 2 个 DocType

## 核心 DocType
- `Communication Medium` — 通信媒介（如电话、邮件、聊天等渠道）
- `Communication Medium Timeslot` — 通信媒介时间段（定义可用时间窗口）

## 与 Telephony 模块的关系
Communication Medium 为 Telephony 模块提供通信渠道定义，Incoming Call Settings 引用 Communication Medium 来路由来电。

## 目录结构
```
communication/
├── doctype/
│   ├── communication_medium/
│   └── communication_medium_timeslot/
└── __init__.py
```
