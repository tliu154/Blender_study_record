---
tags:
  - "#course/Blender"
  - "#type/资料"
created: 2026-11-18
---
# 教学大纲（Syllabus）· 完整骨架

**本文件是整个仓库唯一的章节清单与状态源。** 各篇 README 只写定位和实践方向，
章节增删、状态更新一律改这里，避免多处重复维护。

- 全局章号 01~18 保持稳定，作为跨文件引用的唯一标识；篇只是分组，不参与编号
- 每章只有真正开写时才建 `.md` 文件；本文件里的「文件」列是**预定路径**，不是现存文件
- `[待写]` 章节**不建空壳文件**；框架阶段链接指向它们属正常，自检脚本会跳过
- 本仓库是 **Obsidian 库**：笔记一律 `.md`，按标签规范打 tags，章节之间用相对超链互引
- 与姊妹仓库 [ComfyUI 教学笔记](https://github.com/tliu154/ComfyUI_study_record) 用超链衔接，不复制其内容

状态：`[已完成]` 教学 + 实操 + 自测通过 ｜ `[部分完成]` 只有部分节 ｜
`[待写]` 仅规划（不建文件） ｜ `[选读]` 低优先级，按需跳读

---

## 第 1 篇 ComfyUI 3D 建模 → `01_comfyui_3d/`

前置：[ComfyUI 2D 基础](https://github.com/tliu154/ComfyUI_study_record)（ch01~ch08 概念）。
目标：在 ComfyUI 里用 AI 生成 3D 模型，理解 3D 表示，导出标准格式并衔接 Blender 后处理。

### 第 1 章 3D 生成概览：从 2D 到 3D（3D Generation Overview） · [已完成]

> [教学](01_comfyui_3d/docs/ch01_3d_overview.md) · [实操](01_comfyui_3d/tasks/ch01_task.md)

**本章子概念索引：** 3D 的几种表示（Mesh / 点云 / 体素 / NeRF / 3DGS）· AI 3D 生成的两条路线（图生 / 文生）· ComfyUI 里的 3D 生态 · 典型流程（AI 生成 → Blender 后处理 → 应用）

**节骨架：** 1.1 3D 和 2D 生成有何不同 ｜ 1.2 常见 3D 表示（够用直觉）｜ 1.3 ComfyUI 能做哪些 3D ｜ 1.4 一条完整流程长什么样

### 第 2 章 图生 3D（Image-to-3D） · [已完成]

> [教学](01_comfyui_3d/docs/ch02_img2img3d.md) · [实操](01_comfyui_3d/tasks/ch02_task.md)

**本章子概念索引：** 图生 3D 原理（够用）· 主流模型（TripoSR / Hunyuan3D / InstantMesh 等）· 输入图要求 · 输出格式与质量

**节骨架：** 2.1 一张图怎么变 3D ｜ 2.2 主流方案对比 ｜ 2.3 最小图生 3D 工作流 ｜ 2.4 输入图质量与结果的关系

### 第 3 章 文生 3D（Text-to-3D） · [已完成] [选读]

> [教学](01_comfyui_3d/docs/ch03_text2_3d.md) · [实操](01_comfyui_3d/tasks/ch03_task.md)

**本章子概念索引：** 文生 3D 路线（Score Distillation / 大模型直出）· 与图生 3D 的取舍 · 多视图生成 · 适用场景

**节骨架：** 3.1 只用文字能生成 3D 吗 ｜ 3.2 文生 vs 图生的取舍 ｜ 3.3 最小文生 3D 流程 ｜ 3.4 什么时候用哪条路

### 第 4 章 3D 模型格式与导出（3D Formats & Export） · [已完成]

> [教学](01_comfyui_3d/docs/ch04_formats.md) · [实操](01_comfyui_3d/tasks/ch04_task.md)

**本章子概念索引：** 常见格式（glb / gltf / obj / fbx / ply / stl）· 网格 vs 点云 · 贴图与材质的携带 · 导出节点设置 · 文件体积与优化

**节骨架：** 4.1 一张表看清常见 3D 格式 ｜ 4.2 该导出哪种格式 ｜ 4.3 贴图/材质怎么跟着走 ｜ 4.4 导出避坑（法线/朝向/单位）

### 第 5 章 衔接 Blender：后处理流程（Handoff to Blender） · [已完成]

> [教学](01_comfyui_3d/docs/ch05_handoff.md) · [实操](01_comfyui_3d/tasks/ch05_task.md)

**本章子概念索引：** 为什么 AI 生成的模型要后处理 · 导入 Blender（链到 [ch07](02_blender_basics/docs/ch07_import.md)）· 清理/修复（链到 [ch08](02_blender_basics/docs/ch08_mesh_cleanup.md)）· 重新导出（链到 [ch11](02_blender_basics/docs/ch11_export.md)）

**节骨架：** 5.1 AI 生成模型常见问题 ｜ 5.2 导入与初步检查 ｜ 5.3 最小后处理链路 ｜ 5.4 导出交付（引擎/打印/展示）

---

## 第 2 篇 Blender 基础 → `02_blender_basics/`

前置：无（Blender 零基础可读）。目标：搭完整 Blender 教学大纲，**只把 ComfyUI 3D 后处理用得到的章节写成正文**，其余留 `[待写]` 占位。

> 说明：本篇是「够用导向」——服务第 1 篇的 3D 后处理。想系统学 Blender 的其它领域，按占位章节逐个补。

### 第 6 章 Blender 界面与视图操作（UI & Navigation） · [已完成]

> [教学](02_blender_basics/docs/ch06_ui_navigation.md) · [实操](02_blender_basics/tasks/ch06_task.md)

**本章子概念索引：** 主界面分区 · 3D 视图导航（旋转/平移/缩放）· 物体模式 vs 编辑模式 · 选择操作 · 单位与坐标系

**节骨架：** 6.1 界面长什么样 ｜ 6.2 视图导航三件套 ｜ 6.3 物体模式与编辑模式 ｜ 6.4 选择、坐标与单位

### 第 7 章 导入与检查模型（Import & Inspect） · [已完成]

> [教学](02_blender_basics/docs/ch07_import.md) · [实操](02_blender_basics/tasks/ch07_task.md)

**本章子概念索引：** 导入 glb/gltf/obj/ply · 场景清理（默认立方体）· 检查网格（线框/统计）· 朝向与缩放 · 法线显示

**节骨架：** 7.1 导入 AI 生成的模型 ｜ 7.2 检查模型是否正常 ｜ 7.3 朝向/缩放/位置修正 ｜ 7.4 常见问题（模型太小/看不见）

### 第 8 章 网格清理与修复（Mesh Cleanup） · [已完成]

> [教学](02_blender_basics/docs/ch08_mesh_cleanup.md) · [实操](02_blender_basics/tasks/ch08_task.md)

**本章子概念索引：** 法线（重计算/朝外）· 非流形边 · 合并顶点（Merge by Distance）· 减面（Decimate）· 平滑与细分

**节骨架：** 8.1 AI 模型为什么要清理 ｜ 8.2 法线与朝向修复 ｜ 8.3 去杂面/合并顶点/减面 ｜ 8.4 平滑与细节取舍

### 第 9 章 UV 展开入门（UV Unwrapping Basics） · [已完成]

> [教学](02_blender_basics/docs/ch09_uv.md) · [实操](02_blender_basics/tasks/ch09_task.md)

**本章子概念索引：** UV 是什么（够用）· UV 编辑器 · 自动展开（Smart UV Project）· 标记缝合边 · 何时需要重展 UV

**节骨架：** 9.1 UV 解决什么问题 ｜ 9.2 UV 编辑器与布局 ｜ 9.3 自动展开够用流程 ｜ 9.4 AI 模型何时需要重展

### 第 10 章 材质与贴图入门（Materials & Textures） · [已完成]

> [教学](02_blender_basics/docs/ch10_materials.md) · [实操](02_blender_basics/tasks/ch10_task.md)

**本章子概念索引：** PBR 基础（Base Color / Roughness / Normal）· 材质槽 · 贴图加载与连接（Shader Editor 够用）· 从 AI 模型继承材质

**节骨架：** 10.1 PBR 三张图（够用直觉）｜ 10.2 材质槽与Shader Editor ｜ 10.3 加载/连接贴图 ｜ 10.4 AI 模型自带材质怎么处理

### 第 11 章 导出模型（Export） · [已完成]

> [教学](02_blender_basics/docs/ch11_export.md) · [实操](02_blender_basics/tasks/ch11_task.md)

**本章子概念索引：** 导出 glb/gltf · fbx（游戏引擎）· obj（通用）· stl（3D 打印）· 应用变换与坐标 · 贴图嵌入

**节骨架：** 11.1 导出前检查清单 ｜ 11.2 glb/gltf 导出设置 ｜ 11.3 按用途选格式（引擎/打印/展示）｜ 11.4 贴图嵌入与常见坑

### 第 12 章 渲染出图（Rendering Basics） · [已完成]

> [教学](02_blender_basics/docs/ch12_render.md) · [实操](02_blender_basics/tasks/ch12_task.md)

**本章子概念索引：** 相机 · 灯光（够用）· Eevee vs Cycles · 世界环境/背景 · 输出设置 · 快速出产品图

**节骨架：** 12.1 给模型拍张照 ｜ 12.2 相机与灯光基础 ｜ 12.3 Eevee/Cycles 怎么选 ｜ 12.4 输出设置与出图

### 第 13 章 建模基础（Modeling Basics） · [待写]（占位）

> 预定：`02_blender_basics/docs/ch13_modeling.md` ｜ 实操：`02_blender_basics/tasks/ch13_task.md`
> 基础几何体、挤出、环切、布尔等——3D 后处理不强制需要，按需再填。

### 第 14 章 灯光进阶（Lighting） · [待写]（占位）

> 预定：`02_blender_basics/docs/ch14_lighting.md` ｜ 实操：`02_blender_basics/tasks/ch14_task.md`
> 三点布光、HDRI、光效——出更好看的图时再填。

### 第 15 章 骨骼与绑定（Rigging） · [待写]（占位）

> 预定：`02_blender_basics/docs/ch15_rigging.md` ｜ 实操：`02_blender_basics/tasks/ch15_task.md`
> 骨骼、蒙皮、权重——需要让模型动起来时再填。

### 第 16 章 动画基础（Animation） · [待写]（占位）

> 预定：`02_blender_basics/docs/ch16_animation.md` ｜ 实操：`02_blender_basics/tasks/ch16_task.md`
> 关键帧、时间轴——做动画时再填。

### 第 17 章 材质进阶（Advanced Materials） · [待写]（占位）

> 预定：`02_blender_basics/docs/ch17_material_advanced.md` ｜ 实操：`02_blender_basics/tasks/ch17_task.md`
> 程序化节点、混合材质——基础材质不够用时再填。

### 第 18 章 雕刻（Sculpting） · [待写]（占位）

> 预定：`02_blender_basics/docs/ch18_sculpt.md` ｜ 实操：`02_blender_basics/tasks/ch18_task.md`
> 雕刻笔刷、细节——需要手工塑形时再填。

---

## 附录 → `90_appendix/`

### 附录 A 术语对照表（Glossary：ComfyUI ↔ Blender） · [已完成]

> [教学](90_appendix/docs/appA_glossary.md)
> 两域同名/异名术语对照（Mesh / Latent / UV / 法线 / 采样…），避免被同一词的不同含义绕晕。

### 附录 B 快捷键速查（Shortcuts） · [已完成]

> [教学](90_appendix/docs/appB_shortcuts.md)
> Blender 高频快捷键（视图导航/模式切换/选择/编辑），按用途分组。

### 附录 C 故障排查（Troubleshooting） · [已完成]

> [教学](90_appendix/docs/appC_troubleshooting.md)
> 导入模型看不见、法线反了、贴图丢失、导出到引擎变形等，按「现象 → 原因 → 处理」列。

---

## 写作与实操约定（速览）

- **每章两份文件**：`docs/chNN_*.md`（教学）+ `tasks/chNN_task.md`（实操），同号
- **节锚点**：`<a id="cNN-MM"></a>` + `### 8.2 ...（English）`，索引链 `#cNN-MM`
- **单节结构**：概念定义 → 直觉类比 → 界面/参数 → 常见误区 → 对应实操链接
- **打 tags**：frontmatter 按 course/type/topic/source 四类规范填写；course 一律 `Blender`
- **跨主题/跨仓库**：一律相对超链（本仓库内）或完整 URL（指向 ComfyUI 主仓库），不复制对方内容
- 详细规则见 [CONTRIBUTING.md](CONTRIBUTING.md)，术语见 [NOTATION.md](NOTATION.md)
