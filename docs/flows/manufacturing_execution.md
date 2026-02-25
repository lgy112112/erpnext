# Manufacturing Execution（制造执行）修改导航

## 流程范围

```
BOM -> Production Plan -> Work Order -> Job Card -> Stock Entry (领料/完工)
                                \
                                 -> Material Request -> Purchase Order (缺料采购)
```

## 主要代码入口（按单据）

### BOM 与计划
- `erpnext/manufacturing/doctype/bom/bom.py`
- `erpnext/manufacturing/doctype/production_plan/production_plan.py`

重点生命周期：
- `ProductionPlan.validate()`
- `ProductionPlan.on_submit()`
- `ProductionPlan.on_cancel()`

### 工单与工序执行
- `erpnext/manufacturing/doctype/work_order/work_order.py`
- `erpnext/manufacturing/doctype/job_card/job_card.py`

`WorkOrder` 常改入口：
- `validate()`
- `before_submit()`
- `on_submit()`
- `on_cancel()`
- `update_status()`

### 库存联动（制造关键）
- `erpnext/stock/doctype/stock_entry/stock_entry.py`

制造相关 `Stock Entry` 常见目的：
- `Material Transfer for Manufacture`
- `Manufacture`

## 跨模块联动点

- `erpnext/stock/`：领料、完工入库、估值、SLE/GL
- `erpnext/buying/` + `erpnext/stock/doctype/material_request/`：缺料采购
- `erpnext/controllers/stock_controller.py`：库存/会计公共逻辑
- `erpnext/hooks.py`：定时任务（例如 BOM 成本恢复更新）

## 修改时必须检查的副作用

1. BOM 展开与替代料/多级 BOM 影响
2. 工单状态推进是否与 `Job Card` 完成度一致
3. 制造型 `Stock Entry` 是否正确写入 SLE/GL
4. 缺料场景下 `Material Request` / 采购链路是否仍可生成
5. 取消工单或撤销库存交易时状态是否回退正确

## 常见回归点

- 只改 `Work Order` 状态逻辑，未同步检查 `Stock Entry` 完工回写
- BOM/计划改动后忽略后台成本更新或重算路径
- 制造与普通库存交易共用 `Stock Entry`，修改目的分支时误伤其他场景

## 最小测试清单（建议）

1. `Production Plan` -> `Work Order` -> `Stock Entry (Manufacture)` 正常链路
2. 分步工序（`Job Card`）执行与状态推进
3. 缺料生成 `Material Request` 并进入采购链路
4. 取消工单/取消制造库存交易回滚
5. 多级 BOM 或替代料场景（至少一条）
