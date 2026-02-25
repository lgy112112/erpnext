# ERPNext 项目指南

## 项目概述
ERPNext 是基于 Frappe 框架的开源 ERP 系统（v17.x-develop），采用 Python + JavaScript 全栈架构，使用 MariaDB/PostgreSQL 数据库。

## 技术栈
- 后端: Python 3.14+, Frappe Framework >= 17.0.0
- 前端: JavaScript (Frappe UI), SCSS
- 数据库: MariaDB / PostgreSQL
- 构建: flit (Python), yarn (JS)
- Lint: ruff (line-length=110, indent=tab, quote=double)
- 测试: pytest + frappe test runner, CI via GitHub Actions (MariaDB + PostgreSQL)

## 代码风格
- Python 缩进使用 tab
- 字符串使用双引号
- 行宽限制 110 字符
- ruff 规则: F, E, W, I, UP, B, RUF（详见 pyproject.toml）

## 项目结构
```
erpnext/
├── accounts/          # 会计与财务（185 doctypes, 52 reports）
├── assets/            # 固定资产管理（26 doctypes, 3 reports）
├── buying/            # 采购管理（20 doctypes, 10 reports）
├── crm/               # 客户关系管理（27 doctypes, 9 reports）
├── manufacturing/     # 生产制造（47 doctypes, 22 reports）
├── selling/           # 销售管理（18 doctypes, 23 reports）
├── stock/             # 库存管理（77 doctypes, 49 reports）
├── subcontracting/    # 委外加工（13 doctypes）
├── support/           # 客户支持（11 doctypes, 4 reports）
├── projects/          # 项目管理（15 doctypes, 5 reports）
├── maintenance/       # 维护保养（5 doctypes, 1 report）
├── quality_management/ # 质量管理（16 doctypes, 1 report）
├── setup/             # 系统设置（40 doctypes）
├── controllers/       # 共享业务控制器
├── regional/          # 地区化适配（6 国家/地区）
├── erpnext_integrations/ # 第三方集成（Plaid 等）
├── edi/               # 电子数据交换
├── communication/     # 通信媒介
├── telephony/         # 电话集成
├── bulk_transaction/  # 批量事务处理
├── portal/            # Web 门户
├── shopping_cart/     # 电商购物车
├── utilities/         # 通用工具（4 doctypes）
├── domains/           # 业务领域预设（制造/零售/服务/分销）
├── workspace_sidebar/ # 工作区侧边栏定义（21 个 JSON）
├── desktop_icon/      # 桌面图标定义（23 个 JSON）
├── change_log/        # 版本更新日志（v5-v15）
├── commands/          # CLI 命令扩展
├── config/            # 模块配置文件
├── report_center/     # 报表中心配置
├── patches/           # 数据库迁移补丁（v4.2-v16.0）
├── public/            # 前端静态资源（JS/SCSS/图标）
├── templates/         # 邮件/打印/Web 模板
├── www/               # 公开网页
├── startup/           # 启动引导与通知
├── tests/             # 根级集成测试
├── gettext/           # 翻译提取器
├── locale/            # 本地化文件（多语言 .po）
├── hooks.py           # Frappe 钩子注册（核心入口）
├── modules.txt        # 模块注册清单
├── patches.txt        # 数据库迁移补丁索引
└── exceptions.py      # 自定义异常类
```

## 核心控制器（erpnext/controllers/）
- `accounts_controller.py` — 所有会计单据的基类
- `buying_controller.py` — 采购单据基类
- `selling_controller.py` — 销售单据基类
- `stock_controller.py` — 库存单据基类
- `subcontracting_controller.py` — 委外单据基类
- `taxes_and_totals.py` — 税费与合计计算
- `status_updater.py` — 单据状态流转
- `budget_controller.py` — 预算控制

## 关键文件
- `hooks.py` — Frappe 应用钩子（调度器、文档事件、权限等）
- `modules.txt` — 已注册模块列表
- `patches.txt` — 数据库迁移补丁索引（v4.2-v16.0）
- `pyproject.toml` — Python 依赖与工具配置
- `exceptions.py` — 自定义异常类（PartyFrozen, InvalidAccountCurrency 等）
- `deprecation_dumpster.py` — 已废弃代码管理

## hooks.py 核心配置

### 文档事件钩子（doc_events）
- 全局验证（SLA、事务删除检查）
- 单据特定事件（Sales Invoice 提交/取消、Communication 更新等）
- 地区化钩子（意大利、阿联酋税务处理）

### 调度任务（scheduler_events）
- 每 15 分钟：BOM 成本更新恢复
- 每 30 分钟：库存估值重算
- 每小时：项目提醒、GL/SLE 文档重命名
- 每日：自动邮件摘要、银行交易同步

### 地区化覆盖（regional_overrides）
支持国家：法国、阿联酋、沙特阿拉伯、意大利、澳大利亚、美国

### 其他关键配置
- **命名系列变量**：FY, TFY, ABBR, MM, DD, YY, YYYY, JJJ, WW
- **树形视图 DocType**：Account, Cost Center, Warehouse, Item Group 等 9 个
- **门户路由规则**：/orders, /invoices, /quotations, /shipments 等
- **全局搜索优先级**：Customer, Supplier, Item, Sales Order 等 18 个
- **会计维度支持**：Sales Invoice, Purchase Invoice, Journal Entry 等 50+ 单据

## 数据库迁移系统

### patches.txt
数据库迁移补丁索引，按版本组织：
- `[pre_model_sync]` — 在模式同步前执行的补丁
- 版本目录：v4_2 至 v16_0
- 支持 Python 模块路径和 `execute:` 内联语句

### patches/ 目录
```
patches/
├── v4_2/    # 最早的补丁
├── v10_0/
├── v11_0/
├── v12_0/
├── v13_0/
├── v14_0/
├── v15_0/
└── v16_0/   # 最新版本补丁
```

## 业务领域预设（Domains）

ERPNext 支持按业务类型定制界面和默认设置：

### 可用域
- **Manufacturing** — 制造业（显示 BOM、工单等）
- **Retail** — 零售业（POS、条码等）
- **Services** — 服务业（项目、工时等）
- **Distribution** — 分销业（库存、物流等）

### 配置内容
- 桌面图标显示/隐藏
- 字段折叠规则
- 默认设置值
- 默认门户角色

## 模块文档
各模块详细说明见 `docs/modules/` 目录。

## 常用命令
```bash
# 运行测试
bench run-tests --app erpnext
bench run-tests --module erpnext.accounts

# Lint
ruff check erpnext/
ruff format erpnext/

# 数据库迁移
bench migrate
```
