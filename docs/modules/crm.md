# CRM 模块（客户关系管理）

## 概述
管理销售线索、商机、合同和营销活动。是销售流程的前端入口。

## 规模
- 27 个 DocType
- 9 个报表

## 核心 DocType

### 主数据
- `Lead` — 销售线索
- `Opportunity` — 商机
- `Competitor` — 竞争对手
- `Market Segment` — 市场细分
- `Campaign` — 营销活动

### 合同
- `Contract` — 合同
- `Contract Template` — 合同模板

### 预约
- `Appointment` — 预约
- `Appointment Booking Settings` — 预约设置

### 营销
- `Email Campaign` — 邮件营销活动
- `Campaign Email Schedule` — 营销邮件排程

### 设置
- `CRM Settings` — CRM 全局设置

## 关键报表
- Lead Details（线索详情）
- Sales Funnel（销售漏斗）
- Opportunity Summary by Sales Stage（商机阶段汇总）
- Campaign Efficiency（营销活动效率）
- First Response Time for Opportunity（商机首次响应时间）

## 业务流程
```
Lead → Opportunity → Quotation (Selling 模块)
  ↓
Campaign → Email Campaign
```

## 与 Frappe CRM 的关系
`frappe_crm_api.py` 提供与独立 Frappe CRM 应用的 API 集成接口。

## 目录结构
```
crm/
├── doctype/           # 27 个 DocType
├── report/            # 9 个报表
├── crm_dashboard/     # CRM 仪表盘
├── frappe_crm_api.py  # Frappe CRM 集成 API
└── workspace/         # 工作区
```
