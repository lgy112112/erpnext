# Gettext 模块（翻译提取器）

## 概述

`gettext/` 存放国际化文本提取辅助代码，用于从特定数据源或文件中提取待翻译文本。

这不是主业务流程代码，但当你新增大量用户可见文案（尤其是非标准位置的数据源）时，可能需要同步调整提取逻辑。

## 规模（当前仓库）
- 5 个 Python 文件
- `extractors/` 子目录包含多个提取器

## 关键目录与文件
- `gettext/extractors/incoterms.py`
- `gettext/extractors/uom_data.py`
- `gettext/extractors/lines_from_txt_file.py`

## 何时需要关注

- 新增的业务文案不在标准 DocType 字段/模板路径中
- 新数据文件需要纳入翻译提取流程
- 本地化构建后发现某些文案没有被提取

## 常见风险

- 后端/模板新增文案但未被提取，翻译文件缺失条目
- 自定义数据源文本未纳入 extractor
