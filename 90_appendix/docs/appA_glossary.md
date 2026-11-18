---
tags:
  - "#course/Blender"
  - "#type/笔记"
  - "#topic/术语"
  - "#source/官方文档"
created: 2026-11-18
---
# 附录 A 术语对照表（Glossary：ComfyUI ↔ Blender）

> 前置：无，遇到混淆的词来查 ｜ 状态：`[已完成]` ｜ 所属：`90_appendix/`

**一句话**：本仓库横跨 ComfyUI（AI 生成）和 Blender（3D 后处理）两个领域，
很多词**同名不同义**或**同义不同名**。这张表帮你别被绕晕。完整约定见 [NOTATION](../../NOTATION.md)。

## 一、同名不同义（最易混）

| 词 | ComfyUI 语境 | Blender 语境 |
|---|---|---|
| **模型（Model）** | 神经网络权重（checkpoint / UNET）| 3D 几何模型（Mesh）|
| **采样（Sampling）** | 从噪声去噪生成内容（KSampler）| 渲染时每像素的光线采样数 |
| **latent** | 潜空间张量 | 基本不用这个词 |
| **材质（Material）** | 一般不涉及 | 表面 PBR 属性集合 |
| **加载（Load）** | 加载模型权重 / 图像 | 导入 3D 文件 / 打开图片 |
| **输出（Output）** | 节点的输出端口 | 渲染结果 / 导出文件 |
| **渲染（Render）** | 少见 | 把 3D 场景算成 2D 图 |

> 读到这些词时先确认语境：这句话在讲"AI 生成"还是"3D 后处理"？

## 二、同义不同名（跨领域找对应）

| 概念 | ComfyUI 说法 | Blender 说法 |
|---|---|---|
| 生成/导出物 | 图 / latent / 3D mesh | 物体（Object）/ 网格（Mesh）|
| 颜色信息 | 提示词描述 | 材质 Base Color / 贴图 |
| 控制形状 | 提示词 / 参考图 / ControlNet | 建模 / 网格编辑（顶点边面）|
| 告诉软件怎么做 | 节点连线 | 节点连线（Shader Editor）|
| 复现设置 | seed + 参数 | .blend 文件 + 渲染设置 |

## 三、Blender 核心术语（3D 后处理常用）

| 中文 | English | 一句话 |
|---|---|---|
| 网格 | Mesh | 顶点+边+面组成的 3D 模型 |
| 顶点/边/面 | Vertex / Edge / Face | 网格的基本元素（`1/2/3` 切换）|
| 法线 | Normal | 面朝向哪，决定受光和正反（[ch08](../../02_blender_basics/docs/ch08_mesh_cleanup.md)）|
| UV 坐标 | UV Coordinates | 3D 表面到 2D 贴图的映射（[ch09](../../02_blender_basics/docs/ch09_uv.md)）|
| 材质 | Material | 表面外观配方（节点网络）|
| 贴图 | Texture | 材质用的图片（颜色/粗糙度/法线图）|
| 修改器 | Modifier | 非破坏性处理（如 Decimate 减面）|
| 物体模式 / 编辑模式 | Object / Edit Mode | 整体操作 / 改网格内部（`Tab` 切换）|
| 视图导航 | Orbit / Pan / Zoom | 旋转/平移/缩放视角（[ch06](../../02_blender_basics/docs/ch06_ui_navigation.md)）|
| 渲染引擎 | Eevee / Cycles | 实时 / 光追渲染（[ch12](../../02_blender_basics/docs/ch12_render.md)）|
| 应用变换 | Apply Transform | 把缩放旋转固化进网格（`Ctrl+A`）|

## 四、3D 格式术语

| 格式 | 一句话 | 用途（[ch04](../../01_comfyui_3d/docs/ch04_formats.md)）|
|---|---|---|
| glb / gltf | 几何+材质+贴图，glb 单文件 | 推荐通用/交接 |
| obj | 几何+UV，贴图外链 | 通用交换 |
| fbx | 几何+材质+动画 | 游戏引擎 |
| stl | 仅表面几何 | 3D 打印 |
| ply | 几何+颜色，点云常用 | 点云/扫描 |

---

## 小结

- 最易混：ComfyUI 的"模型"=权重，Blender 的"模型"=几何；"采样"在两边含义完全不同。
- Blender 高频词：网格/法线/UV/材质/修改器/两种模式——配合链接章节理解。
- 遇到不确定的词，先判断语境再查表。

> 回 [附录首页](../README.md) ｜ 回 [仓库首页](../../README.md)
