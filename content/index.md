## 任务
```base
columns:
  - file.name
  - file.folder
  - file.mtime
sort:
  - field: file.mtime
    order: desc
filters:
  and:
    - file.tags.contains("task")
    - file.path.startsWith("05-task")
views:
  - type: table
    name: 待办任务
    filters:
      and:
        - 任务状态.containsAny("🚧 Doing", "📝 Todo")
    order:
      - file.name
      - 任务状态
      - 关联领域
      - 计划时间
      - 关联项目
    columnSize:
      file.name: 260
      note.任务状态: 123
      note.关联领域: 130
      note.计划时间: 169
  - type: table
    name: 待排期任务
    filters:
      and:
        - 任务状态 == ["⏳ Waiting"]

```
## 项目
```base
columns:
  - file.name
  - file.folder
  - file.mtime
  - 关联领域
filters:
  and:
    - file.tags.contains("project")
    - '!file.path.contains("99-system")'
views:
  - type: table
    name: 所有项目
    order:
      - file.name
      - 项目状态
      - 关联领域
    columnSize:
      file.name: 293
      note.项目状态: 120
      note.关联领域: 237
  - type: table
    name: 活跃项目
    filters:
      and:
        - 项目状态 == ["🚧 Doing"]
    order:
      - file.name
      - 项目状态
      - 关联领域
      - 计划时间
    sort: []
    columnSize:
      file.name: 262
      note.项目状态: 120
      note.关联领域: 134

```
## 领域
```base
columns:
  - file.name
  - file.folder
  - file.mtime
sort:
  - field: file.mtime
    order: desc
filters:
  and:
    - file.tags.contains("area")
    - '!file.path.startsWith("99-system")'
formulas:
  领域项目数: ""
  笔记数: ""
properties:
  formula.领域项目数:
    displayName: 项目数
views:
  - type: table
    name: 领域
    order:
      - file.name
      - 领域状态
      - formula.领域项目数
      - formula.笔记数
      - file.path
    sort:
      - property: formula.领域项目数
        direction: ASC
    columnSize:
      file.name: 209
      note.领域状态: 119
      formula.领域项目数: 111
      formula.笔记数: 121

```
