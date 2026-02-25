# Portal 模块（Web 门户）

## 概述
为客户和供应商提供 Web 自助门户，可查看订单、发票等单据。

## 规模
- 2 个 DocType

## 核心 DocType
- `Website Attribute` — 网站属性（用于产品筛选）
- `Website Filter Field` — 网站筛选字段

## 关键文件
- `utils.py` — 门户工具函数（如 `create_customer_or_supplier`，在用户登录时自动创建客户/供应商记录）

## 与 Shopping Cart 的关系
Portal 模块提供基础的门户功能，Shopping Cart 模块在此基础上实现购物车和在线下单。

## 目录结构
```
portal/
├── doctype/
│   ├── website_attribute/
│   └── website_filter_field/
└── utils.py
```
