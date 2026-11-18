---
tags:
  - "#course/Blender"
  - "#type/笔记"
  - "#topic/快捷键"
  - "#source/官方文档"
created: 2026-11-18
---
# 附录 B 快捷键速查（Shortcuts）

> 前置：无，操作时来查 ｜ 状态：`[已完成]` ｜ 所属：`90_appendix/`

**一句话**：Blender 靠快捷键提高效率，这里按**用途分组**列 3D 后处理最高频的那些。
快捷键比菜单路径更稳定（跨版本变化小），值得记。

> 提示：以下为常见默认快捷键，个别可能在偏好设置里被改过；菜单里都有对应项可查。

## 一、视图导航（[ch06 6.2](../../02_blender_basics/docs/ch06_ui_navigation.md#c06-02)）

| 操作 | 快捷键 |
|---|---|
| 旋转视角 Orbit | 按住**鼠标中键**拖动 |
| 平移视角 Pan | `Shift` + 中键拖动 |
| 缩放 Zoom | 滚轮 |
| 框选全部（找模型）| `Home` |
| 聚焦选中 | 小键盘 `.` |
| 切到相机视角 | 小键盘 `0` |

## 二、模式与选择（[ch06 6.3](../../02_blender_basics/docs/ch06_ui_navigation.md#c06-03)）

| 操作 | 快捷键 |
|---|---|
| 物体模式 ⇄ 编辑模式 | `Tab` |
| 全选 / 取消全选 | `A` / `Alt+A` |
| 切顶点 / 边 / 面 | `1` / `2` / `3`（编辑模式）|
| 点选 | 鼠标左键 |

## 三、物体变换（[ch07 7.3](../../02_blender_basics/docs/ch07_import.md#c07-03)）

| 操作 | 快捷键 |
|---|---|
| 移动 Grab | `G`（+ `X/Y/Z` 限轴）|
| 旋转 Rotate | `R` |
| 缩放 Scale | `S` |
| 确认 / 取消 | 左键或 `Enter` / `Esc` |
| 清除位置/旋转/缩放 | `Alt+G` / `Alt+R` / `Alt+S` |
| 应用变换 | `Ctrl+A` → Scale / Rotation |

## 四、网格编辑（[ch08](../../02_blender_basics/docs/ch08_mesh_cleanup.md)）

| 操作 | 快捷键 |
|---|---|
| 重算法线朝外 | `Shift+N`（编辑模式）|
| 合并顶点 | `M` → Merge by Distance |
| 删除（面/边/点）| `X` → 选类型 |
| 由边/顶点填面 | `F` |
| 添加修改器 | 属性面板扳手图标 → Add Modifier（Decimate 减面）|

## 五、UV 与材质（[ch09](../../02_blender_basics/docs/ch09_uv.md) / [ch10](../../02_blender_basics/docs/ch10_materials.md)）

| 操作 | 快捷键 |
|---|---|
| UV 映射菜单（含 Smart UV Project）| `U`（编辑模式）|
| 添加节点（Shader Editor）| `Shift+A` |
| 标记缝合边 | `Ctrl+E`（进阶）|

## 六、渲染与文件

| 操作 | 快捷键 |
|---|---|
| 渲染 | `F12` |
| 保存文件 | `Ctrl+S` |
| 打开文件 | `Ctrl+O` |
| 撤销 | `Ctrl+Z` |
| 打包外部资源（贴图）| `File > External Data > Pack Resources`（菜单，无默认快捷键）|

---

## 小结

- 导航三件套（中键转 / Shift+中键移 / 滚轮缩放）+ `Home` 是最高频，先记这组。
- `Tab` 切模式、`G/R/S` 变换、`A` 全选——三大通用操作。
- 后处理专用：`Shift+N` 修法线、`M` 合并顶点、`U` 展 UV、`Ctrl+A` 应用变换。

> 回 [附录首页](../README.md) ｜ 回 [仓库首页](../../README.md)
