# Controllers 模块（共享业务控制器）

## 概述
`controllers/` 不是一个 Frappe 模块，而是存放跨模块共享的业务逻辑控制器。所有交易单据通过继承这些控制器获得通用能力。

## 继承层次
```
TransactionBase (utilities/transaction_base.py)
  └── AccountsController (accounts_controller.py)
        └── StockController (stock_controller.py)
              ├── SubcontractingController (subcontracting_controller.py)
              │     └── BuyingController (buying_controller.py)
              └── SellingController (selling_controller.py)
```

## 核心控制器

### accounts_controller.py
所有含会计分录的单据的基类，提供：
- 税费行处理
- 多币种金额计算
- 预算校验
- 预付款处理
- 会计维度（Accounting Dimension）处理

### buying_controller.py
采购单据基类（Purchase Order, Purchase Receipt, Purchase Invoice），提供：
- 采购特有的税费逻辑
- 供应商物料编号映射
- 原材料供应（委外）

### selling_controller.py
销售单据基类（Quotation, Sales Order, Delivery Note, Sales Invoice），提供：
- 销售佣金计算
- 信用额度校验
- 产品捆绑展开

### stock_controller.py
库存单据基类，提供：
- Stock Ledger Entry 创建
- 库存估值
- 序列号/批次处理
- 会计分录联动（永续盘存）

### taxes_and_totals.py
税费与合计计算引擎，被所有交易单据调用：
- 逐行税费计算
- 折扣处理
- 四舍五入调整
- 净额/含税额转换

### status_updater.py
单据状态流转引擎：
- 基于子单据完成度更新父单据状态
- 超额交付/收款校验
- 关闭/重开单据

### budget_controller.py
预算控制逻辑，在单据提交时校验预算。

### queries.py
通用的 Link Field 查询函数（供前端下拉搜索使用）。

### sales_and_purchase_return.py
销售退货和采购退货的公共逻辑。

### item_variant.py
物料变体管理逻辑，处理基于模板的变体创建。

### subcontracting_inward_controller.py
委外入库控制器，处理委外收货的特殊逻辑。

### print_settings.py
打印设置自定义，提供额外的打印配置选项。

### website_list_for_contact.py
门户列表过滤，根据联系人权限过滤 Web 表单列表。

### trends.py
趋势分析报表的公共逻辑。
