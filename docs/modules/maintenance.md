# Maintenance 模块（维护保养）

## 概述
管理设备/产品的定期维护计划和维护访问记录。

## 规模
- 5 个 DocType
- 1 个报表

## 核心 DocType
- `Maintenance Schedule` — 维护计划（定义周期性维护任务）
- `Maintenance Schedule Item` — 维护计划明细
- `Maintenance Schedule Detail` — 维护计划详情（生成的具体日期）
- `Maintenance Visit` — 维护访问记录
- `Maintenance Visit Purpose` — 维护访问目的

## 业务流程
```
Sales Order (含维护计划) → Maintenance Schedule → Maintenance Visit
```

## 目录结构
```
maintenance/
├── doctype/           # 5 个 DocType
└── report/            # 1 个报表
```
