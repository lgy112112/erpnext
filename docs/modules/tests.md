# Tests 模块（根级测试入口）

## 概述

`erpnext/tests/` 是根级测试入口，主要放跨模块、回归型、系统级测试与公共测试工具。

注意：
- ERPNext 还有大量模块内测试（例如各模块 `doctype/*/test_*.py`）
- 修改主业务流程时，通常需要同时看根级测试和目标模块测试

## 规模（根级目录）
- 10 个 Python 文件（含测试与工具）

## 当前根级测试文件（示例）
- `erpnext/tests/test_regional.py` — 地区化回归
- `erpnext/tests/test_point_of_sale.py` — POS 相关回归
- `erpnext/tests/test_notifications.py` — 通知相关
- `erpnext/tests/test_webform.py` — Web Form 行为
- `erpnext/tests/utils.py` — 测试辅助函数

## 修改主业务流程时的测试策略

1. 优先补目标单据所在模块的测试
- 例如改 `Sales Order`，先看 `selling/doctype/sales_order/` 下测试

2. 再补跨模块回归
- 销售/采购/库存/会计联动
- 地区化覆盖（如 UAE / Italy）

3. 若改了 Web/Portal 流程
- 同步检查 `erpnext/tests/test_webform.py`
- 检查 `templates/` 与 `www/` 对应页面

## 常见风险

- 只改代码不补测试，后续状态回写或金额计算回归难发现
- 只测提交流程，不测取消流程（ERPNext 很多 bug 出在回滚）
- 忽略部分交付/部分开票/部分收货场景
