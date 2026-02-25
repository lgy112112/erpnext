# Config 模块（模块配置入口）

## 概述

`config/` 是模块配置入口目录。当前仓库该目录内容较少，但仍是定位模块配置/导航定义的潜在入口之一。

## 规模（当前仓库）
- 1 个 Python 文件：`config/projects.py`

## 用途

当你修改模块导航、配置入口或历史配置代码时，可先检查本目录是否有对应定义。

## 备注

ERPNext 很多 UI/工作区配置已更多转向 JSON（如 `workspace_sidebar/`, `desktop_icon/`），因此 `config/` 在当前版本不是主要改动点，但排查时不要遗漏。
