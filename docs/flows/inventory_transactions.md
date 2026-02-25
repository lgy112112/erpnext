# Inventory Transactions（库存交易与估值）修改导航

## 范围

本流程关注库存数量与估值的核心副作用，而不是某个单据的业务前台流程。

关键目标：
- 生成正确的 `Stock Ledger Entry (SLE)`
- 在永续盘存下生成正确的 GL 分录
- 正确维护 `Bin` 汇总数量/估值
- 支持重算与回滚

## 关键单据与文件

### 直接写库存的核心单据
- `erpnext/stock/doctype/stock_entry/stock_entry.py`
- `erpnext/stock/doctype/stock_reconciliation/stock_reconciliation.py`
- `erpnext/stock/doctype/purchase_receipt/purchase_receipt.py`
- `erpnext/stock/doctype/delivery_note/delivery_note.py`
- `erpnext/subcontracting/doctype/subcontracting_receipt/subcontracting_receipt.py`

### 库存公共逻辑
- `erpnext/controllers/stock_controller.py`
  - `make_sl_entries()`
  - `make_gl_entries()`
  - `get_gl_entries()`
- `erpnext/stock/stock_ledger.py`
- `erpnext/stock/valuation.py`
- `erpnext/stock/stock_balance.py`
- `erpnext/stock/serial_batch_bundle.py`

### 重算与后台任务
- `erpnext/stock/doctype/repost_item_valuation/repost_item_valuation.py`
- `erpnext/hooks.py` 中 `scheduler_events`（重算任务）

## `Stock Entry` 特别注意

`Stock Entry` 是库存与制造/委外联动的核心单据，常见入口：
- `validate()`
- `on_submit()`
- `on_cancel()`
- `update_stock_ledger()`
- `get_gl_entries()`

修改 `Stock Entry` 时必须同时考虑：
- 领料/转移/生产入库等不同 `purpose`
- 序列号与批次校验
- 是否允许负库存
- 永续盘存下 GL 联动
- `hooks.py` 中对 `Material Request` 完成度的回写

## 修改时必须检查的副作用

1. SLE 顺序与数量符号是否正确（入库/出库）
2. `Bin` 汇总数量是否与 SLE 一致
3. 估值方法（FIFO / Moving Average）结果是否变化
4. 永续盘存下 GL 分录是否匹配库存变化
5. 取消单据后 SLE/GL 回滚是否完整
6. 重算任务（repost）是否仍可处理历史数据

## 常见回归点

- 只改前台校验，未改 `update_stock_ledger()` 导致账本仍旧行为
- 忽略 `serial_batch_bundle` 约束，序列号/批次场景报错
- 改了估值逻辑未验证历史重算任务
- 出库/入库符号或仓库方向处理错误，造成 `Bin` 异常

## 最小测试清单（建议）

1. `Stock Entry`（转移/调整/生产）提交与取消
2. `Purchase Receipt` / `Delivery Note` 的库存影响与回滚
3. 序列号/批次物料交易
4. FIFO 与移动平均估值场景
5. 重算（repost item valuation）至少一条回归
