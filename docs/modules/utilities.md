# Utilities 模块（通用工具）

## 概述
存放跨模块共用的工具 DocType 和函数。

## 规模
- 4 个 DocType

## 核心 DocType
- `Video` — 视频（产品/培训视频管理）
- `Video Settings` — 视频设置（YouTube API 集成）
- `SMS Settings` — 短信设置
- `Rename Tool` — 批量重命名工具

## 关键文件
- `activation.py` — 系统激活状态检查（引导用户完成基础设置）
- `bulk_transaction.py` — 批量事务处理工具函数
- `product.py` — 产品相关工具函数
- `transaction_base.py` — 交易单据基础工具（AccountsController 的基类）
- `naming.py` — 命名规则工具函数
- `regional.py` — 地区化工具函数

## 目录结构
```
utilities/
├── doctype/           # 4 个 DocType
├── report/            # 报表
├── web_form/          # Web 表单
├── activation.py      # 激活检查
├── bulk_transaction.py # 批量处理
├── naming.py          # 命名规则
├── product.py         # 产品工具
├── regional.py        # 地区化工具
└── transaction_base.py # 交易单据基类
```
