# Telephony 模块（电话集成）

## 概述
管理电话系统集成，支持来电处理、通话记录和语音通话设置。

## 规模
- 5 个 DocType

## 核心 DocType
- `Call Log` — 通话记录
- `Voice Call Settings` — 语音通话设置
- `Incoming Call Settings` — 来电处理设置
- `Incoming Call Handling Schedule` — 来电处理排程
- `Telephony Call Type` — 通话类型

## 用途
与 VoIP/PBX 系统集成，自动记录通话、弹屏显示客户信息、按时间段路由来电到不同处理人。

## 目录结构
```
telephony/
├── doctype/
│   ├── call_log/
│   ├── voice_call_settings/
│   ├── incoming_call_settings/
│   ├── incoming_call_handling_schedule/
│   └── telephony_call_type/
└── __init__.py
```
