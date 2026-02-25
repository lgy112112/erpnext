# Desktop Icon 模块（桌面图标配置）

## 概述

`desktop_icon/` 存放桌面模块图标与分组 JSON 配置，和 `public/desktop_icons/*.svg` 资源配合使用。

当你新增模块入口、调整模块分组或图标展示时，需要同时检查这里和 `public/desktop_icons/`。

## 规模（当前仓库）
- 23 个 JSON 文件

## 常见文件（示例）
- `desktop_icon/selling.json`
- `desktop_icon/buying.json`
- `desktop_icon/stock.json`
- `desktop_icon/manufacturing.json`
- `desktop_icon/accounting.json`

## 常见风险

- 新模块入口只改了工作区侧栏，未改桌面图标
- 图标 JSON 与实际 SVG 资源名称不一致
