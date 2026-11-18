---
tags:
  - "#course/Blender"
  - "#type/资料"
created: 2026-11-18
---
# 术语与命名约定（Notation）

全仓库统一。本仓库横跨 ComfyUI（AI 生成）与 Blender（3D 后处理）两个领域，
同一词在不同领域含义可能不同，首次出现务必写清语境；完整对照见 [附录 A](90_appendix/docs/appA_glossary.md)。

## 1. 通用写法

- **中文（English）** 首次出现：如「网格（Mesh）」「法线（Normal）」，之后可只用中文或英文
- **界面原文**：Blender 的菜单/节点/按钮名、ComfyUI 的节点/端口名，保留界面英文原文，
  需要时括号补中文，如「Decimate 修改器」「`Export glTF`」
- **菜单路径**：用 `文件 > 导入 > glTF 2.0`（Blender）或 `Workflow > Browse Templates`（ComfyUI）的 `>` 分隔写法
- **数值/单位**：数字与单位间留空格（如 `2.0 秒`、`1024×1024`）；Blender 默认单位米，注明场景单位设置

## 2. 缩写表

| 缩写 | 全称 | 说明 |
|---|---|---|
| AI3D | AI-generated 3D | AI 生成的 3D 内容 |
| Mesh | 网格 | 由顶点/边/面组成的 3D 模型表示 |
| UV | UV 坐标 | 把 2D 贴图映射到 3D 表面的坐标 |
| PBR | Physically Based Rendering | 基于物理的渲染，材质工作流 |
| glTF / glb | GL Transmission Format | 3D 场景/模型交换格式，glb 为二进制单文件 |
| NeRF | Neural Radiance Fields | 神经辐射场，一种 3D 表示 |
| 3DGS | 3D Gaussian Splatting | 3D 高斯泼溅，一种新型 3D 表示 |
| SDF | Signed Distance Field | 有向距离场 |

## 3. 易混词（重点）

同一词在两个领域含义不同，写作时注意区分——

| 词 | ComfyUI 语境 | Blender 语境 |
|---|---|---|
| **采样（Sampling）** | 从噪声一步步去噪出图/3D 的过程（KSampler）| 渲染时每个像素的光线采样数 |
| **模型（Model）** | 神经网络权重（checkpoint / UNET）| 3D 几何模型（Mesh）|
| ** latent ** | 潜空间张量 | Blender 里基本不用，避免混用 |
| **材质（Material）** | 一般不涉及 | 物体表面的 PBR 属性集合 |
| **精度 / 分辨率** | 出图尺寸 / 模型精度(fp8) | 渲染分辨率 / 网格细分数 |

> 规则：出现易混词时，句内点明「在 ComfyUI 里指…」「在 Blender 里指…」，别让读者自己猜。

## 4. 常用节点名速查（ComfyUI 3D）

保留界面英文原文：

- 图生 3D 相关节点名随节点包不同（TripoSR / Hunyuan3D / InstantMesh 等），以实际安装为准
- 导出相关：常见的 3D 输出/保存节点按所用节点包命名，写作时给通用思路 + 当下具体节点名

## 5. 常用界面名速查（Blender）

保留界面英文原文（中文菜单按你本地界面补）：

- 模式：`Object Mode`（物体模式）/ `Edit Mode`（编辑模式）/ `Sculpt Mode`（雕刻模式）
- 视图导航：`Orbit`（旋转）/ `Pan`（平移）/ `Zoom`（缩放）
- 编辑：`Merge by Distance`（按距离合并）/ `Recalculate Normals`(Shift+N) / `Decimate`（减面）
- UV：`Smart UV Project`（智能 UV 投射）/ `Mark Seam`（标记缝合边）
- 材质：`Shader Editor`（着色器编辑器）/ `Base Color` / `Roughness` / `Normal`
- 导出：`Export glTF 2.0` / `Export FBX` / `Export OBJ` / `Export STL`
- 渲染：`Eevee` / `Cycles` / `Camera` / `World`

> 节点名/菜单名会随 Blender 版本变化，写作时注明「以你使用的版本为准」，
> 关键操作给出快捷键（快捷键比菜单路径更稳定）。
