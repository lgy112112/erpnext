# Procure-to-Pay（采购到付款）修改导航

## 流程范围

```
Material Request -> Request for Quotation -> Supplier Quotation
                                         -> Purchase Order
                                         -> Purchase Receipt
                                         -> Purchase Invoice
                                         -> Payment Entry
```

## 主要代码入口（按单据）

### 采购前置
- `erpnext/stock/doctype/material_request/material_request.py`
- `erpnext/buying/doctype/request_for_quotation/request_for_quotation.py`
- `erpnext/buying/doctype/supplier_quotation/supplier_quotation.py`

重点生命周期：
- `MaterialRequest.validate()`
- `MaterialRequest.before_submit() / on_submit() / before_cancel() / on_cancel()`
- `MaterialRequest.update_status()`

### 采购订单与收货
- `erpnext/buying/doctype/purchase_order/purchase_order.py`
- `erpnext/stock/doctype/purchase_receipt/purchase_receipt.py`

重点生命周期：
- `PurchaseOrder.validate() / on_submit() / on_cancel() / update_status()`
- `PurchaseReceipt.validate() / on_submit() / before_cancel() / on_cancel()`
- `PurchaseReceipt.update_status() / update_billing_status()`
- `PurchaseReceipt.get_gl_entries()`（永续盘存）

### 采购发票与付款
- `erpnext/accounts/doctype/purchase_invoice/purchase_invoice.py`
- `erpnext/accounts/doctype/payment_entry/payment_entry.py`

重点生命周期：
- `PurchaseInvoice.validate() / before_submit() / on_submit() / on_cancel()`
- `PurchaseInvoice.make_gl_entries()`
- `PurchaseInvoice.set_status()`

## 公共控制器与联动点

- `erpnext/controllers/buying_controller.py`
  - 采购税费、供应商相关通用逻辑、委外相关联动
- `erpnext/controllers/subcontracting_controller.py`
  - 委外流程的库存/消耗联动基础逻辑
- `erpnext/controllers/stock_controller.py`
  - 收货与库存会计联动（SLE/GL）
- `erpnext/controllers/accounts_controller.py`
  - 采购发票会计逻辑、取消回滚
- `erpnext/controllers/status_updater.py`
  - 上游单据状态回写、数量/金额约束

## `hooks.py` 中与采购链路相关的额外副作用

- `Stock Entry` 的提交/取消会触发：
  - `erpnext.stock.doctype.material_request.material_request.update_completed_and_requested_qty`
- `Purchase Invoice` 可能受 UAE 地区化校验影响（`doc_events.validate`）

## 修改时必须检查的副作用

1. 请购/订单/收货/开票状态回写是否一致
2. 部分收货、部分开票时数量与金额状态是否正确
3. 永续盘存下 `Purchase Receipt` 与 `Purchase Invoice` 的 GL 行为是否符合预期
4. 委外场景是否被意外影响（`SubcontractingController`）
5. 取消单据后上游单据状态与未清数量是否恢复

## 常见回归点

- 只改 `Purchase Order` 逻辑，忽略 `Purchase Receipt.update_billing_status()`
- 修改 `Material Request` 完成度规则，但遗漏 `hooks.py` 中 `Stock Entry` 回写
- 改采购发票金额逻辑后未验证税费引擎与多币种
- 委外采购与普通采购共用控制器逻辑，改动误伤委外流程

## 最小测试清单（建议）

1. 标准采购：请购 -> 询价 -> 订单 -> 收货 -> 发票 -> 付款
2. 部分收货 / 部分开票回写
3. 取消 `Purchase Receipt` / `Purchase Invoice` 回滚
4. 永续盘存下 GL 行为校验
5. 委外采购回归（至少一条）
