# Stock 模块（库存管理）

## 概述
管理物料、仓库、库存交易和物流。是 ERPNext 中第二大模块，与 Accounts、Buying、Selling、Manufacturing 模块深度集成。

## 规模
- 77 个 DocType
- 49 个报表

## 核心 DocType

### 主数据
- `Item` — 物料主数据（支持变体、批次、序列号）
- `Item Group` — 物料分组（树形）
- `Warehouse` — 仓库（树形结构）
- `Price List` — 价格表
- `Item Price` — 物料价格
- `Batch` — 批次
- `Serial No` — 序列号
- `UOM` — 计量单位
- `Manufacturer` — 制造商
- `Brand` — 品牌

### 交易单据
- `Material Request` — 物料需求申请
- `Purchase Receipt` — 采购入库单
- `Delivery Note` — 发货单
- `Stock Entry` — 库存调拨/调整/生产入库
- `Stock Reconciliation` — 库存盘点调整
- `Pick List` — 拣货单
- `Packing Slip` — 装箱单
- `Shipment` — 发运单
- `Delivery Trip` — 配送行程

### 库存核算
- `Bin` — 仓库-物料库存汇总（实时余额）
- `Stock Ledger Entry` — 库存账本分录
- `Landed Cost Voucher` — 到岸成本分摊

### 质量
- `Quality Inspection` — 质量检验

## 关键报表
- Stock Balance（库存余额）
- Stock Ledger（库存账本）
- Stock Ageing（库存账龄）
- Stock Projected Qty（预计库存）
- Item-wise Price List Rate（物料价格表）
- Warehouse-wise Stock Balance（仓库库存余额）
- Batch-wise Balance History（批次余额历史）
- Serial No Ledger（序列号台账）

## 架构要点

### 永续盘存
库存交易自动生成 Stock Ledger Entry，并通过 `StockController` 联动生成会计分录（GL Entry），实现永续盘存。

### 估值方法
支持 FIFO（先进先出）和 Moving Average（移动加权平均）两种库存估值方法，在 Item 或 Warehouse 级别配置。

### 控制器继承
库存单据继承 `StockController`（位于 `controllers/stock_controller.py`），处理：
- 库存账本分录
- 库存估值
- 序列号/批次校验
- 会计分录联动

## 目录结构
```
stock/
├── doctype/                    # 77 个 DocType
├── report/                     # 49 个报表
├── dashboard/                  # 仪表板配置
├── dashboard_chart/            # 仪表板图表
├── dashboard_chart_source/     # 图表数据源
├── number_card/                # 数字卡片
├── workspace/                  # 工作区定义
├── page/                       # 自定义页面
├── print_format/               # 打印格式
├── spec/                       # 规格说明
├── stock_ledger.py             # 库存账本核心逻辑
├── stock_balance.py            # 库存余额计算
├── serial_batch_bundle.py      # 序列号/批次处理
├── get_item_details.py         # 获取物料详情（被多模块调用）
├── valuation.py                # 估值计算
├── reorder_item.py             # 再订购点管理
└── utils.py                    # 库存工具函数
```
