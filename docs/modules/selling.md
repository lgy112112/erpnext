# Selling 模块（销售管理）

## 概述
管理销售流程，从报价到销售订单。与 Accounts（销售发票）、Stock（发货单）模块联动。

## 规模
- 18 个 DocType
- 23 个报表

## 核心 DocType

### 主数据
- `Customer` — 客户主数据
- `Sales Partner Type` — 销售伙伴类型
- `Industry Type` — 行业类型
- `Product Bundle` — 产品组合（虚拟捆绑销售）

### 交易单据
- `Quotation` — 报价单
- `Sales Order` — 销售订单
- `Installation Note` — 安装记录

### 设置
- `Selling Settings` — 销售模块全局设置

## 关键报表
- Sales Analytics（销售分析）
- Sales Order Analysis（销售订单分析）
- Quotation Trends（报价趋势）
- Customer Acquisition and Loyalty（客户获取与忠诚度）
- Item-wise Sales History（物料销售历史）
- Sales Person-wise Transaction Summary（销售员交易汇总）
- Territory-wise Sales（区域销售）

## 业务流程
```
Lead → Opportunity → Quotation → Sales Order → Delivery Note → Sales Invoice
                                      ↓
                                 Production Plan (制造型企业)
```

## 控制器
销售单据继承 `SellingController`（`controllers/selling_controller.py`），处理：
- 销售税费计算
- 销售团队佣金
- 信用额度校验
- 定价规则应用

## 目录结构
```
selling/
├── doctype/           # 18 个 DocType
├── report/            # 23 个报表
├── selling_dashboard/ # 模块仪表盘
├── dashboard_chart/   # 仪表盘图表
├── number_card/       # 数字卡片
├── page/              # 销售漏斗等页面
├── print_format/      # 打印格式
├── print_format_field_template/ # 打印格式字段模板
└── workspace/         # 工作区
```
