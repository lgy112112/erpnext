# EDI 模块（电子数据交换）

## 概述
支持 EDI（Electronic Data Interchange）标准，用于企业间的电子化单据交换。

## 规模
- 2 个 DocType

## 核心 DocType
- `Code List` — 代码表（EDI 标准代码集合）
- `Common Code` — 通用代码（代码表中的具体代码项）

## 用途
EDI 代码表用于标准化企业间数据交换中的编码（如国家代码、货币代码、计量单位代码等），确保不同系统间的数据互通。

## 目录结构
```
edi/
├── doctype/
│   ├── code_list/     # 代码表
│   └── common_code/   # 通用代码
└── __init__.py
```
