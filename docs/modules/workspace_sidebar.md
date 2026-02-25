# Workspace Sidebar 模块（工作区侧边栏配置）

## 概述

`workspace_sidebar/` 存放工作区侧边栏 JSON 配置，决定左侧导航分组、条目和展示结构。

当业务流程变更涉及工作区入口、菜单组织、功能曝光时，需要同步修改这里。

## 规模（当前仓库）
- 21 个 JSON 文件

## 常见文件（示例）
- `workspace_sidebar/selling.json`
- `workspace_sidebar/buying.json`
- `workspace_sidebar/stock.json`
- `workspace_sidebar/manufacturing.json`
- `workspace_sidebar/accounts_setup.json`

## 修改业务流程时必须检查

- 新单据/报表是否需要在工作区侧栏暴露
- 功能重命名后侧栏标签是否同步
- 不同业务域下是否需要调整入口顺序

## 常见风险

- 后端功能已改，但工作区入口未更新，用户找不到功能
- 旧菜单仍指向已弃用路径/名称
