# Regional 模块（地区化适配）

## 概述
处理各国/地区特有的税务、法规和报表需求。包含国家级别的定制逻辑和合规报表。

## 规模
- 5 个 DocType
- 6 个国家/地区子目录

## 核心 DocType
- `Import Supplier Invoice` — 导入供应商发票（意大利电子发票）
- `Lower Deduction Certificate` — 低扣税证书（印度 TDS）
- `South Africa VAT Settings` — 南非增值税设置
- `UAE VAT Settings` / `UAE VAT Account` — 阿联酋增值税设置

## 支持的国家/地区

### 有专用目录的国家
- **Australia**（澳大利亚）
- **Italy**（意大利）— 电子发票（SDI 集成）、税务处理
- **South Africa**（南非）— 增值税合规
- **Turkey**（土耳其）
- **United Arab Emirates**（阿联酋）— 反向征税机制
- **United States**（美国）— IRS 1099 表单

### 通过 regional_overrides 支持
- **France**（法国）
- **Saudi Arabia**（沙特阿拉伯）

## 架构要点
地区化逻辑通过 `hooks.py` 中的 `regional_overrides` 注入到核心流程中，避免在核心代码中硬编码国家特定逻辑。

## 目录结构
```
regional/
├── doctype/              # 地区化 DocType
├── report/               # 地区化报表
├── print_format/         # 税务发票打印格式
├── address_template/     # 地址模板
├── australia/
├── italy/
├── south_africa/
├── turkey/
├── united_arab_emirates/
└── united_states/
```
