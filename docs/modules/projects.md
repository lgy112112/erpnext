# Projects 模块（项目管理）

## 概述
管理项目、任务和工时记录。支持项目模板、任务依赖和成本跟踪。

## 规模
- 15 个 DocType
- 5 个报表

## 核心 DocType
- `Project` — 项目（关联客户、销售订单）
- `Task` — 任务（支持依赖关系、甘特图）
- `Project Template` — 项目模板（快速创建标准项目）
- `Timesheet` — 工时记录（关联项目/任务，可计费）
- `Activity Type` — 活动类型
- `Activity Cost` — 活动成本（按员工和活动类型定义费率）
- `Project Type` — 项目类型
- `Project Update` — 项目进度更新

## 关键报表
- Project Summary（项目汇总）
- Daily Timesheet Summary（每日工时汇总）
- Project Profitability（项目盈利分析）
- Project-wise Stock Tracking（项目库存跟踪）

## 与其他模块集成
- Accounts: Timesheet 可生成 Sales Invoice（计费工时）
- Selling: 项目可关联销售订单
- Buying: 项目可关联采购订单进行成本归集

## 目录结构
```
projects/
├── doctype/           # 15 个 DocType
├── report/            # 5 个报表
├── dashboard_chart/   # 仪表盘图表
└── number_card/       # 数字卡片
```
