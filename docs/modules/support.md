# Support 模块（客户支持）

## 概述
管理售后服务，包括工单（Issue）、SLA 和保修索赔。

## 规模
- 11 个 DocType
- 4 个报表

## 核心 DocType
- `Issue` — 工单/问题（客户支持的核心单据）
- `Issue Type` — 工单类型
- `Issue Priority` — 工单优先级
- `Service Level Agreement` — 服务级别协议（SLA）
- `Warranty Claim` — 保修索赔
- `Support Settings` — 支持模块设置
- `Support Search Source` — 知识库搜索源

### SLA 相关
- `Service Level Priority` — SLA 优先级定义
- `Pause SLA on Status` — 暂停 SLA 的状态
- `SLA Fulfilled on Status` — SLA 达成的状态

## 关键报表
- First Response Time for Issues（工单首次响应时间）
- Support Hours（支持工时）

## 目录结构
```
support/
├── doctype/           # 11 个 DocType
├── report/            # 4 个报表
├── page/              # 支持页面
└── workspace/         # 工作区
```
