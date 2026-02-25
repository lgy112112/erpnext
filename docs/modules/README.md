# ERPNext 模块索引（核心业务 + 变更支撑）

> 说明：本目录不是 `erpnext/` 顶层目录的全量镜像，而是优先覆盖“业务流程修改”和“核心联动排查”常用模块。

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

## 变更支撑模块（建议给 LLM 一并加载）

| 模块 | 目录 | 说明 |
|------|------|------|
| [迁移补丁](patches.md) | `patches/` | 数据库迁移脚本与版本补丁入口 |
| [测试入口](tests.md) | `tests/` | 根级测试与跨模块回归检查 |
| [前端静态资源](public.md) | `public/` | JS Bundle、表单控制器、前端联动代码 |
| [模板系统](templates.md) | `templates/` | 邮件/打印/Web 页面模板与页面脚本 |
| [网站路由页面](www.md) | `www/` | `www/` 路由页面实现（Python + HTML/JS/CSS） |
| [启动与通知](startup.md) | `startup/` | Boot、通知、首页卡片与过滤 |
| [领域预设](domains.md) | `domains/` | 不同行业域的界面/功能预设 |
| [模块配置](config.md) | `config/` | 模块级配置入口（当前较少） |
| [工作区侧栏](workspace_sidebar.md) | `workspace_sidebar/` | 工作区侧边栏 JSON 配置 |
| [桌面图标](desktop_icon.md) | `desktop_icon/` | 桌面模块图标与分组配置 |
| [报表中心配置](report_center.md) | `report_center/` | 报表中心 JSON 配置 |

## 工程与国际化支撑模块（按需加载）

| 模块 | 目录 | 说明 |
|------|------|------|
| [变更日志](change_log.md) | `change_log/` | 历史版本发布说明与功能变更记录 |
| [CLI 命令入口](commands.md) | `commands/` | Bench/命令扩展入口（当前内容很少） |
| [翻译提取器](gettext.md) | `gettext/` | i18n 文本提取辅助代码 |
| [本地化资源](locale.md) | `locale/` | 多语言 `.po` / `.pot` 翻译文件 |

## 流程修改导航（新增）

当目标是“修改主业务流程”，建议同时阅读 `docs/flows/`：

- `docs/flows/README.md` — 流程导航总览
- `docs/flows/sell_to_cash.md` — 销售到回款（S2C）
- `docs/flows/procure_to_pay.md` — 采购到付款（P2P）
- `docs/flows/inventory_transactions.md` — 库存交易与估值联动
- `docs/flows/manufacturing_execution.md` — 制造执行与库存/采购联动

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
