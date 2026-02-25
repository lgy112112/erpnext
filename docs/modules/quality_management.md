# Quality Management 模块（质量管理）

## 概述
实现质量管理体系（QMS），包括质量目标、质量反馈、质量行动、质量会议和质量程序。

## 规模
- 16 个 DocType
- 1 个报表

## 核心 DocType
- `Quality Goal` — 质量目标（含可量化的目标指标）
- `Quality Review` — 质量评审（对质量目标的定期评审）
- `Quality Action` — 质量行动（纠正/预防措施）
- `Quality Feedback` — 质量反馈（客户/内部反馈）
- `Quality Feedback Template` — 反馈模板
- `Quality Meeting` — 质量会议
- `Quality Procedure` — 质量程序（SOP 文档，树形结构）
- `Non Conformance` — 不合格项

## 与 Stock 模块的关系
质量检验（Quality Inspection）定义在 Stock 模块中，可在采购入库、生产入库时触发。

## 目录结构
```
quality_management/
├── doctype/           # 16 个 DocType
├── report/            # 1 个报表
└── workspace/         # 工作区
```
