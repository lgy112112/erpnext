# ERPNext 模块索引

## 核心业务模块

| 模块 | 目录 | DocType 数 | 报表数 | 说明 |
|------|------|-----------|--------|------|
| [会计与财务](accounts.md) | `accounts/` | 185 | 52 | 复式记账、发票、收付款、银行对账 |
| [库存管理](stock.md) | `stock/` | 77 | 49 | 物料、仓库、出入库、库存估值 |
| [生产制造](manufacturing.md) | `manufacturing/` | 47 | 22 | BOM、工单、工序、产能规划 |
| [销售管理](selling.md) | `selling/` | 18 | 23 | 客户、报价、销售订单 |
| [采购管理](buying.md) | `buying/` | 20 | 10 | 供应商、询价、采购订单 |
| [CRM](crm.md) | `crm/` | 27 | 9 | 线索、商机、合同、营销活动 |
| [固定资产](assets.md) | `assets/` | 26 | 3 | 资产生命周期、折旧、维护 |
| [委外加工](subcontracting.md) | `subcontracting/` | 13 | — | 委外订单、委外收货 |

## 辅助业务模块

| 模块 | 目录 | DocType 数 | 说明 |
|------|------|-----------|------|
| [项目管理](projects.md) | `projects/` | 15 | 项目、任务、工时 |
| [客户支持](support.md) | `support/` | 11 | 工单、SLA、保修 |
| [维护保养](maintenance.md) | `maintenance/` | 5 | 维护计划、维护访问 |
| [质量管理](quality_management.md) | `quality_management/` | 16 | 质量目标、评审、行动 |

## 基础设施模块

| 模块 | 目录 | 说明 |
|------|------|------|
| [系统设置](setup.md) | `setup/` | 公司、货币、安装向导（40 doctypes）|
| [控制器](controllers.md) | `controllers/` | 共享业务逻辑基类 |
| [地区化](regional.md) | `regional/` | 各国税务与法规适配（6 国家）|
| [通用工具](utilities.md) | `utilities/` | 跨模块工具函数（4 doctypes）|

## 集成与通信模块

| 模块 | 目录 | 说明 |
|------|------|------|
| [第三方集成](erpnext_integrations.md) | `erpnext_integrations/` | Plaid 银行集成等 |
| [EDI](edi.md) | `edi/` | 电子数据交换代码表 |
| [通信媒介](communication.md) | `communication/` | 通信渠道定义 |
| [电话集成](telephony.md) | `telephony/` | VoIP/通话记录 |
| [批量事务](bulk_transaction.md) | `bulk_transaction/` | 批量单据生成 |
| [Web 门户](portal.md) | `portal/` | 客户/供应商自助门户 |
| [购物车](shopping_cart.md) | `shopping_cart/` | 电商购物车与在线下单 |

## 模块间依赖关系

```
CRM → Selling → Stock → Accounts
                  ↑
Buying ──────────┘
                  ↑
Manufacturing ───┘
                  ↑
Subcontracting ──┘

Assets → Accounts
Projects → Accounts (Timesheet 计费)
Support (独立，通过 Customer 关联)
```
