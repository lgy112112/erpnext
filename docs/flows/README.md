# ERPNext 主业务流程修改导航

本目录面向“让 LLM 修改业务流程代码”而设计，重点提供：

- 流程对应的核心 DocType 与代码入口
- 生命周期方法（`validate` / `on_submit` / `on_cancel`）
- 状态回写、税费计算、库存/会计副作用
- 常见回归点与最小测试清单

## 推荐阅读顺序

1. `docs/modules/controllers.md`（公共控制器与方法级入口）
2. 目标流程文档（本目录）
3. 目标模块文档（`docs/modules/*.md`）
4. `CLAUDE.md`（项目级 hooks / scheduler / patches 背景）

## 流程清单

- `sell_to_cash.md`：销售到回款（Lead/Opportunity → Quotation → Sales Order → Delivery Note → Sales Invoice → Payment Entry）
- `procure_to_pay.md`：采购到付款（Material Request/RFQ → Supplier Quotation → Purchase Order → Purchase Receipt → Purchase Invoice → Payment Entry）
- `inventory_transactions.md`：库存交易（SLE/GL/估值/重算）
- `manufacturing_execution.md`：制造执行（BOM/Production Plan/Work Order/Job Card/Stock Entry）
