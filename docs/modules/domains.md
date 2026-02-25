# Domains 模块（业务领域预设）

## 概述

`domains/` 用于定义不同行业场景下的功能/界面预设（如制造、零售、服务、分销）。

业务流程修改如果涉及“在某些行业域启用/禁用功能”，需要检查这里。

## 规模（当前仓库）
- 5 个 Python 文件（含 `__init__.py`）
- 4 个主要领域定义：`manufacturing`, `retail`, `services`, `distribution`

## 关键文件
- `domains/manufacturing.py`
- `domains/retail.py`
- `domains/services.py`
- `domains/distribution.py`

## 修改业务流程时何时需要看这里

- 新功能只对特定行业域可见
- 菜单/模块显示范围需要按行业域控制
- 默认配置因行业域不同而变化

## 常见风险

- 业务功能代码已上线，但对应 domain 未开放入口
- 只在默认域验证，忽略制造/零售等域差异
