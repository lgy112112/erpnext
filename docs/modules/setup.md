# Setup 模块（系统设置）

## 概述
ERPNext 的基础设置模块，包含公司、员工、货币、命名规则等全局配置，以及安装向导。

## 规模
- 40 个 DocType

## 核心 DocType

### 组织架构
- `Company` — 公司（多公司支持，树形结构）
- `Department` — 部门
- `Designation` — 职位
- `Branch` — 分支机构

### 基础设置
- `Currency` / `Currency Exchange` — 货币与汇率
- `Territory` — 销售区域（树形）
- `Sales Person` — 销售员（树形）
- `Customer Group` — 客户分组（树形）
- `Supplier Group` — 供应商分组（树形）
- `Item Group` — 物料分组（树形，定义在 Stock 模块）

### 命名与编号
- `Naming Series` — 编号规则

### 打印与品牌
- `Print Heading` — 打印标题
- `Terms and Conditions` — 条款与条件
- `Brand Defaults` — 品牌默认值

### 安装向导
- `setup_wizard/` — 安装向导（首次安装时的引导配置）
- `demo.py` / `demo_data/` — 演示数据生成

## 目录结构
```
setup/
├── doctype/           # 40 个 DocType
├── setup_wizard/      # 安装向导
├── demo.py            # 演示数据
├── demo_data/         # 演示数据文件
├── install.py         # 安装后初始化
└── utils.py           # 设置工具函数
```
