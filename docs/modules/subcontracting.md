# Subcontracting 模块（委外加工）

## 概述
管理委外加工流程：向供应商发送原材料，接收加工后的成品/半成品。

## 规模
- 13 个 DocType

## 核心 DocType
- `Subcontracting BOM` — 委外 BOM（定义原材料与成品的对应关系）
- `Subcontracting Order` — 委外订单（向供应商下达加工指令）
- `Subcontracting Receipt` — 委外收货单（接收加工成品，消耗原材料）
- `Subcontracting Inward Order` — 委外入库订单

## 业务流程
```
Subcontracting BOM → Subcontracting Order → (发料给供应商)
                                                    ↓
                                          Subcontracting Receipt (收回成品)
```

## 控制器
- `SubcontractingController`（`controllers/subcontracting_controller.py`）— 处理原材料消耗和成品入库
- `SubcontractingInwardController`（`controllers/subcontracting_inward_controller.py`）— 处理入库逻辑

## 目录结构
```
subcontracting/
├── doctype/           # 13 个 DocType
├── dashboard_chart/   # 仪表盘图表
├── number_card/       # 数字卡片
└── workspace/         # 工作区
```
