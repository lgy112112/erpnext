# Shopping Cart 模块（电商购物车）

## 概述
提供电商购物车功能，支持在线下单、购物车管理和结账流程。

## 规模
- 无独立 DocType（复用 Portal 和 Selling 模块的 DocType）
- 无独立 Web Template（基础设施模块）

## 核心功能
- 购物车会话管理
- 在线下单（生成 Quotation/Sales Order）
- 产品浏览与筛选
- 结账流程

## 与其他模块的关系
- 依赖 Portal 模块提供基础门户功能
- 生成 Selling 模块的 Quotation 和 Sales Order
- 使用 Stock 模块的 Item 和 Price List

## 目录结构
```
shopping_cart/
├── doctype/           # 空（无独立 DocType）
├── web_template/      # 基础设施（仅 __init__.py）
└── __init__.py        # 模块初始化
```
