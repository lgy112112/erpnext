# Assets 模块（固定资产管理）

## 概述
管理固定资产的全生命周期：采购、折旧、维护、移动、报废和资本化。

## 规模
- 26 个 DocType
- 3 个报表（另有 2 个在 Accounts 模块）

## 核心 DocType

### 主数据
- `Asset Category` — 资产类别（关联折旧方法和会计科目）
- `Location` — 资产位置

### 资产生命周期
- `Asset` — 资产主记录
- `Asset Depreciation Schedule` — 折旧计划表
- `Asset Movement` — 资产移动（调拨、领用、归还）
- `Asset Repair` — 资产维修
- `Asset Capitalization` — 资产资本化（将费用转为资产）
- `Asset Value Adjustment` — 资产价值调整

### 维护
- `Asset Maintenance` — 资产维护计划
- `Asset Maintenance Log` — 维护日志
- `Asset Maintenance Team` — 维护团队

### 跟踪
- `Asset Activity` — 资产活动日志

## 关键报表
- Fixed Asset Register（固定资产台账）
- Asset Depreciation Ledger（折旧台账，在 Accounts 模块）
- Asset Depreciations and Balances（折旧与余额，在 Accounts 模块）

## 架构要点

### 折旧方法
支持直线法（Straight Line）、递减余额法（Written Down Value）、双倍余额递减法等。通过 `Asset Finance Book` 支持多账簿下不同折旧策略。

### 与 Accounts 集成
资产采购通过 Purchase Invoice/Receipt 创建，折旧自动生成 Journal Entry，报废/出售生成对应会计分录。

## 目录结构
```
assets/
├── doctype/           # 26 个 DocType
├── dashboard_chart/   # 仪表盘图表
└── workspace/         # 工作区
```
