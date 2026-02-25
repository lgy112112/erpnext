# WWW 模块（网站路由页面）

## 概述

`www/` 是 Frappe/ERPNext 的文件系统路由页面目录。这里的页面通常直接对应站点 URL，常见组合为：
- `index.py`
- `index.html`
- `index.js`
- `index.css`

当业务流程涉及 Portal/网站入口（预约、支持、商品列表等）时，通常需要同步检查这里。

## 规模（当前仓库）
- 约 19 个文件
- 包含 Python/HTML/JS/CSS 混合页面实现

## 已存在页面（示例）
- `www/book_appointment/` — 预约页面（含 `index.py/html/js/css`）
- `www/support/` — 支持页面
- `www/payment_setup_certification.py/.html`
- `www/all-products/`, `www/shop-by-category/`

## 修改业务流程时何时需要看 `www`

- 新增或修改面向客户/供应商的 Web 提交入口
- 修改 Portal 页面表单字段与后端处理逻辑
- 修改 URL 页面展示或权限行为

## 常见风险

- 只改 DocType API，不改 `www/` 页面提交字段
- `www/` 页面与 `templates/` include 片段字段不一致
- 页面 JS 仍依赖旧接口返回结构
