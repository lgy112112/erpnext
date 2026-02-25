# Sell-to-Cash（销售到回款）修改导航

## 流程范围

```
Lead / Opportunity (CRM)
    -> Quotation
    -> Sales Order
    -> Delivery Note
    -> Sales Invoice
    -> Payment Entry
```

## 主要代码入口（按单据）

### 销售前置（CRM）
- `erpnext/crm/doctype/lead/lead.py`
- `erpnext/crm/doctype/opportunity/opportunity.py`

### 报价与订单
- `erpnext/selling/doctype/quotation/quotation.py`
- `erpnext/selling/doctype/sales_order/sales_order.py`

重点生命周期：
- `validate()`
- `on_submit()`
- `on_cancel()`
- `update_status()`（`Sales Order`）

### 发货与开票
- `erpnext/stock/doctype/delivery_note/delivery_note.py`
- `erpnext/accounts/doctype/sales_invoice/sales_invoice.py`

重点生命周期：
- `validate()`
- `before_submit()`
- `on_submit()`
- `before_cancel()`
- `on_cancel()`
- `update_billing_status()`（`Delivery Note`）
- `make_gl_entries()`（`Sales Invoice`）
- `set_status()`（`Sales Invoice`）

### 收款
- `erpnext/accounts/doctype/payment_entry/payment_entry.py`

## 公共控制器与联动点

- `erpnext/controllers/selling_controller.py`
  - 信用额度、销售团队佣金、销售侧税费逻辑
- `erpnext/controllers/stock_controller.py`
  - 永续盘存场景下库存与会计联动
- `erpnext/controllers/accounts_controller.py`
  - 会计维度、税费汇总、多币种、GL 相关通用逻辑
- `erpnext/controllers/taxes_and_totals.py`
  - 价格/税费/折扣总计算
- `erpnext/controllers/status_updater.py`
  - 上游单据完成度、开票状态、数量约束

## 修改时必须检查的副作用

1. 状态回写
- `Sales Order` 是否被 `Delivery Note` / `Sales Invoice` 回写完成度
- `Delivery Note` 开票状态是否正确更新

2. 金额与税费
- 折扣、含税/未税转换、四舍五入是否仍正确
- 地区化税务覆盖是否影响结果（见 `hooks.py` 的 `regional_overrides`）

3. 库存与会计
- `Delivery Note` / `Sales Invoice` 在永续盘存配置下是否触发预期 GL/SLE
- 取消单据时是否完整回滚

4. 预付款/收款链路
- `Payment Entry` 与订单/发票的关联和核销状态是否受影响

## 常见回归点

- 只改 `Sales Order` 状态字段，忘记 `status_updater.py` 会覆盖状态
- 只改 `Sales Invoice` 金额字段，忘记税费引擎重算会再次改写
- 修改交付/开票逻辑后，取消流程 (`on_cancel`) 未同步回滚
- 忽略 `hooks.py` 中 `Sales Invoice` 的地区化 `doc_events`

## 最小测试清单（建议）

1. 报价 -> 销售订单 -> 发货 -> 开票 -> 收款 正常链路
2. 部分发货 / 部分开票的状态与数量回写
3. 取消 `Delivery Note` / `Sales Invoice` 后状态与账务回滚
4. 含税价、折扣、多币种场景金额一致性
5. 有地区化配置（如 UAE/Italy）时的回归验证
