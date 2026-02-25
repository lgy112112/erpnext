# Buying 模块（采购管理）

## 概述
管理采购流程，从询价到采购订单。与 Stock（采购入库）、Accounts（采购发票）模块联动。

## 规模
- 20 个 DocType
- 10 个报表

## 核心 DocType

### 主数据
- `Supplier` — 供应商主数据
- `Supplier Scorecard` — 供应商评分卡
- `Buying Settings` — 采购模块全局设置

### 交易单据
- `Material Request` — 物料需求申请（定义在 Stock 模块，但采购流程起点）
- `Request for Quotation` — 询价单
- `Supplier Quotation` — 供应商报价
- `Purchase Order` — 采购订单

## 关键报表
- Purchase Analytics（采购分析）
- Purchase Order Analysis（采购订单分析）
- Supplier Quotation Comparison（供应商报价对比）
- Requested Items to Order and Receive（待下单/待收货物料）
- Subcontracted Item to be Received（待收委外物料）

## 业务流程
```
Material Request → Request for Quotation → Supplier Quotation
                                                    ↓
                                            Purchase Order → Purchase Receipt → Purchase Invoice
```

## 控制器
采购单据继承 `BuyingController`（`controllers/buying_controller.py`），处理：
- 采购税费计算
- 供应商评分更新
- 物料需求关联
- 定价规则应用

## 目录结构
```
buying/
├── doctype/           # 20 个 DocType
├── report/            # 10 个报表
├── buying_dashboard/  # 模块仪表盘
├── dashboard_chart/   # 仪表盘图表
├── number_card/       # 数字卡片
├── page/              # 自定义页面
├── print_format/      # 打印格式
├── print_format_field_template/ # 打印格式字段模板
└── workspace/         # 工作区
```
