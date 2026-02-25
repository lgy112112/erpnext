# Public 模块（前端静态资源与表单脚本）

## 概述

`public/` 存放 ERPNext 前端静态资源，尤其是：
- 前端 JS bundle
- 表单控制器脚本（客户端行为）
- 前端模板片段
- 图标与图片资源

当你修改业务流程时，如果涉及前端表单行为、按钮、查询、前端校验，通常需要同步修改这里。

## 规模（当前仓库）
- 约 146 个文件
- 其中 JS 文件约 52 个

## 关键子目录

### `public/js/`
高频修改区域，包含：
- `controllers/*.js` — 客户端表单控制器（accounts / buying / stock 等）
- `controllers/taxes_and_totals.js` — 客户端税费/金额联动
- `queries.js` — 常用查询逻辑
- `utils/*.js` — 通用前端辅助
- 各功能 bundle（如 POS、BOM configurator、bank reconciliation）

### `public/desktop_icons/`
- 模块图标 SVG 资源，与 `desktop_icon/*.json` 配套

### `public/images/`
- 网站与 UI 图片资源

## 修改业务流程时何时需要看 `public/js`

- 新增/修改按钮、前端动作
- 表单字段联动与默认值变化
- 前端查询过滤条件变化
- 税费/金额即时计算显示不一致
- Portal/Web 页面前端脚本变更

## 常见风险

- 只改后端 `validate/on_submit`，忘了前端表单仍按旧规则校验/提示
- 服务端字段名变更，客户端脚本仍读旧字段
- 税费逻辑后端已改，客户端 `taxes_and_totals.js` 表现不一致
