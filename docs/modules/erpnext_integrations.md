# ERPNext Integrations 模块（第三方集成）

## 概述
管理 ERPNext 与外部服务的集成，目前主要是 Plaid 银行数据集成。

## 规模
- 1 个 DocType

## 核心 DocType
- `Plaid Settings` — Plaid 银行数据集成设置（自动同步银行交易）

## 依赖
- `plaid-python` — Plaid API 客户端
- `googlemaps` — Google Maps API（地址验证）
- `python-youtube` — YouTube API

## 目录结构
```
erpnext_integrations/
├── doctype/
│   └── plaid_settings/  # Plaid 集成配置
├── custom/              # 自定义扩展
└── utils.py             # 集成工具函数
```
