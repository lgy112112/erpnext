# Accounts 模块（会计与财务）

## 概述
ERPNext 最大的核心模块，实现传统复式记账系统。所有财务数据最终汇入 General Ledger（总账）和 Payment Ledger（付款账本）。

## 规模
- 185 个 DocType
- 52 个报表
- 19 个打印格式

## 核心 DocType

### 主数据
- `Account` — 会计科目（树形结构，即"科目表 Chart of Accounts"）
- `Cost Center` — 成本中心（树形结构）
- `Finance Book` — 财务账簿（支持多账簿并行）
- `Fiscal Year` — 会计年度
- `Budget` — 预算
- `Bank` / `Bank Account` — 银行与银行账户

### 交易单据
- `Journal Entry` — 日记账分录
- `Sales Invoice` — 销售发票（含明细行）
- `Purchase Invoice` — 采购发票（含明细行）
- `Payment Entry` — 收付款单
- `Payment Request` — 付款请求
- `Payment Reconciliation` — 收付款核销
- `Dunning` — 催款单

### 银行相关
- `Bank Transaction` — 银行交易流水
- `Bank Reconciliation Tool` — 银行对账工具
- `Bank Statement Import` — 银行对账单导入
- `Bank Clearance` — 银行清算

### 税务与定价
- `Tax Rule` — 税务规则
- `Tax Withholding Category` — 预扣税类别
- `Pricing Rule` — 定价规则
- `Shipping Rule` — 运费规则

### 期末处理
- `Period Closing Voucher` — 期末结转凭证
- `Exchange Rate Revaluation` — 汇率重估
- `Process Deferred Accounting` — 递延收入/费用处理

## 关键报表
- Balance Sheet（资产负债表）
- Profit and Loss Statement（损益表）
- Cash Flow（现金流量表）
- Trial Balance（试算平衡表）
- General Ledger（总账明细）
- Accounts Receivable / Payable（应收/应付账款）
- Budget Variance Report（预算差异报告）

## 架构要点

### Payment Ledger
应收/应付类型的交易同时写入 Payment Ledger，用 `account_type` + `amount`（正/负）替代传统的借/贷字段，`against_voucher_no` 关联原始单据，便于快速计算未清余额。

### 控制器继承
所有会计单据继承 `AccountsController`（位于 `controllers/accounts_controller.py`），提供：
- 税费计算
- 多币种处理
- 预算校验
- 总账分录生成

## 目录结构
```
accounts/
├── doctype/                    # 185 个 DocType 定义
├── report/                     # 52 个报表
├── custom/                     # 对 Frappe 核心 DocType 的扩展（Address）
├── print_format/               # 19 个打印格式
├── dashboard_chart/            # 仪表板图表
├── dashboard_chart_source/     # 图表数据源
├── number_card/                # 数字卡片
├── workspace/                  # 工作区定义
├── page/                       # 自定义页面
├── letterhead/                 # 信头模板
├── notification/               # 通知配置
├── party.py                    # 客户/供应商公共逻辑
├── general_ledger.py           # 总账分录核心逻辑
├── utils.py                    # 工具函数
└── deferred_revenue.py         # 递延收入处理
```
