# 设计文档索引

## 目的

`docs/design/` 存放稳定的应用层所有者文档。

此目录用于：

- 产品功能基准
- 页面与流程行为
- 角色与权限
- 应用壳行为

使用 `docs/architecture/` 存放跨领域的技术结构。

## 范围边界

- `docs/requirements/` 归当前切片应构建的内容所有
- `docs/design/` 归该切片验收后的稳定应用层基准所有
- `docs/architecture/` 归技术设计与跨功能结构所有

当某个功能既依赖业务设计又依赖技术设计时，请将这两个关注点放在不同的文件中，并相互建立交叉引用。

## 起始文件

- `app-overview.md`
- `feature-inventory.md`
- `roles-and-permissions.md`
