# Manufacturing 模块（生产制造）

## 概述
管理生产计划、物料清单（BOM）、工单、工序和产能规划。与 Stock 模块紧密集成，生产入库/领料通过 Stock Entry 完成。

## 规模
- 47 个 DocType
- 22 个报表

## 核心 DocType

### 主数据
- `BOM`（Bill of Materials）— 物料清单（树形，支持多级嵌套）
- `BOM Creator` — BOM 可视化创建工具
- `Workstation` / `Workstation Type` — 工作站
- `Operation` — 工序定义
- `Routing` — 工艺路线

### 生产计划
- `Production Plan` — 生产计划（从销售订单/物料需求生成）
- `Material Request Plan Item` — 物料需求计划明细

### 生产执行
- `Work Order` — 工单
- `Job Card` — 工序卡（跟踪每道工序的执行）
- `Stock Entry` — 领料/入库（类型: Material Transfer for Manufacture / Manufacture）

### 其他
- `Blanket Order` — 一揽子订单（框架协议）
- `Downtime Entry` — 停机记录
- `BOM Update Tool` / `BOM Update Log` — BOM 批量更新

## 关键报表
- Production Planning Report（生产计划报告）
- BOM Stock Report（BOM 库存报告）
- Work Order Summary（工单汇总）
- Job Card Summary（工序卡汇总）
- Cost of Poor Quality（质量成本）
- Production Analytics（生产分析）

## 架构要点

### BOM 结构
BOM 支持多级嵌套（子装配件），通过 `BOM Explosion Item` 展开为扁平物料清单。支持多版本 BOM 和默认 BOM 设置。

### 生产流程
```
Production Plan → Work Order → Job Card → Stock Entry (Manufacture)
                                ↓
                          Material Request → Purchase Order
```

### 产能规划
通过 Workstation 的可用时间和 Operation 的工时定义，在 Production Plan 中进行产能校验。

## 目录结构
```
manufacturing/
├── doctype/           # 47 个 DocType
├── report/            # 22 个报表
├── manufacturing_dashboard/ # 模块仪表盘
├── dashboard_chart/   # 仪表盘图表
├── dashboard_fixtures.py # 仪表盘预设数据
├── notification/      # 通知配置
├── number_card/       # 数字卡片
├── page/              # 自定义页面
└── workspace/         # 工作区配置
```
