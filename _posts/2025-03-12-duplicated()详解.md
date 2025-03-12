---
title: duplicated()详解
description: >-
  duplicated() 是用于检测数据中重复项的函数。
author: 刘十五
date: 2025-03-12 12:30:00 +0800
categories: [Blogging, Tutorial]
tags: [Python笔记]
pin: true
media_subpath: '/posts/20250312'
---

`duplicated()` 是用于检测数据中重复项的函数，常见于数据处理场景（如 Pandas 库）和数据库操作中。以下是其核心功能及参数的详解：

---

### **1. 基本功能**

- **作用**：`duplicated()` 返回一个布尔数组（`True`/`False`），标识数据中的重复行[3][5]。

  - 默认情况下，若某行的所有列值与之前的某行完全一致，则标记为 `True`（即重复项）[1]。

  - 例如，在 Pandas 中调用 `df.duplicated()` 会返回一个布尔序列，表示每一行是否重复[3][5]。

---

### **2. 参数详解**

#### **（1）`subset`**

- **用途**：指定检测重复项的范围。

- **默认值**：所有列（即全列匹配才视为重复）[1]。

- **示例**：`df.duplicated(subset=['列名1', '列名2'])` 仅检查指定列是否重复[1]。

#### **（2）`keep`**

- **用途**：控制标记重复项的规则。

- **可选值**：

  - `'first'`（默认）：将重复项的首次出现标记为 `False`（即非重复），后续重复项标记为 `True`[1]。

  - `'last'`：将最后一次出现的重复项标记为 `False`，其余重复项标记为 `True`[1]。

  - `False`：所有重复项均标记为 `True`[1]。

- **示例**：`df.duplicated(keep='last')` 会保留最后一次出现的重复项，其余标记为重复[1]。

---

### **3. 常见应用场景**

- **查找重复项**：通过 `df[df.duplicated()]` 筛选出重复行[3][5]。

- **删除重复项**：配合 `drop_duplicates()` 使用，例如 `df.drop_duplicates(keep='first')` 删除重复行，仅保留首次出现的数据[3][8]。

- **数据库操作**：类似功能也存在于 SQL 或 RMAN 工具中，例如 MySQL 的 `ON DUPLICATE KEY UPDATE` 用于处理键冲突时的更新操作[19]，或 RMAN 的 `DUPLICATE` 命令创建数据库副本[4]。

---

### **4. 与其他函数的关联**

- **`drop_duplicates()`**：直接删除重复项，参数与 `duplicated()` 类似（如 `subset` 和 `keep`）[8]。

- **数据库工具**：如 `pt-duplicate-key-checker` 可检测数据库中的重复索引[13]。

---

### **总结**

`duplicated()` 是数据清洗的关键工具，通过灵活设置 `subset` 和 `keep` 参数，可精准控制重复项的识别逻辑。结合 `drop_duplicates()` 能高效完成去重操作[1][3][5][8]。在数据库领域，类似概念用于索引检查或副本管理[4][13][19]。

