# Bulk Transaction 模块（批量事务处理）

## 概述
提供批量创建下游单据的能力，如从多个销售订单批量生成发货单或发票。

## 规模
- 2 个 DocType

## 核心 DocType
- `Bulk Transaction Log` — 批量事务日志（记录批量操作的执行结果）
- `Bulk Transaction Log Detail` — 批量事务日志明细

## 用途
当需要从大量源单据（如销售订单、采购订单）批量生成目标单据时，通过此模块异步执行并记录结果，避免逐单手动操作。

## 目录结构
```
bulk_transaction/
├── doctype/
│   ├── bulk_transaction_log/
│   └── bulk_transaction_log_detail/
└── __init__.py
```
