---
tags:
  - "#course/Blender"
  - "#type/笔记"
  - "#topic/材质"
  - "#source/官方文档"
created: 2026-11-18
---
# 第 10 章 材质与贴图入门（Materials & Textures）

> 前置：[ch09 UV](ch09_uv.md)（要贴图片图时需先有 UV）｜ 对应实操：[`ch10_task.md`](../tasks/ch10_task.md)
> 状态：`[已完成]` ｜ 所属篇：`02_blender_basics/`

**一句话**：材质决定模型表面"看起来是什么"——颜色、粗糙度、金属感、凹凸；
最常用的是 **PBR 三张图**（颜色/粗糙度/法线贴图），贴到材质节点上，模型就从白模变成品。

> 本篇一条线：[ch06 界面](ch06_ui_navigation.md) → [ch07 导入](ch07_import.md) → [ch08 网格清理](ch08_mesh_cleanup.md) → [ch09 UV](ch09_uv.md) → [ch10 材质](ch10_materials.md) → [ch11 导出](ch11_export.md) → [ch12 渲染](ch12_render.md)。

## 本章子概念索引

| 概念 | 小节 |
|---|---|
| [PBR 三张图（够用直觉）](#c10-01) | 10.1 |
| [材质槽与 Shader Editor](#c10-02) | 10.2 |
| [加载/连接贴图](#c10-03) | 10.3 |
| [AI 模型自带材质怎么处理](#c10-04) | 10.4 |

---

<a id="c10-01"></a>

### 10.1 PBR 三张图（够用直觉）

**概念定义**：PBR（基于物理的渲染）是现代材质的主流方式。最常用的三张贴图：
**Base Color（基础色）**=物体本来的颜色花纹；
**Roughness（粗糙度）**=表面多粗糙（高=磨砂，低=镜面）；
**Normal（法线贴图）**=伪造表面凹凸细节（不用加真实几何）。
三张图组合，就能表现绝大多数真实材质。

**直觉类比**：像**给模型化妆**——
Base Color 是粉底（决定肤色/花纹），
Roughness 是散粉（决定哑光还是油亮），
Normal 是阴影修容（不用真动骨头，就显出立体纹理）。
三步下去，素颜白模变精致成品。

**界面 / 参数**：三张图速查——
| 贴图 | 接哪个输入 | 作用 |
|---|---|---|
| **Base Color / Albedo** | Base Color | 颜色/花纹（不含光影）|
| **Roughness** | Roughness | 0=镜面，1=全磨砂 |
| **Normal** | Normal（经 Normal Map 节点）| 伪造凹凸细节 |

- 金属物体还常配 **Metallic** 贴图/值（0=非金属，1=金属）

**常见误区**：
- ❌「Base Color 图里带阴影更好看」—— 不。颜色图应是"无光影的纯颜色"，光影交给渲染算。
- ❌「法线贴图就是普通图片直接接」—— 要经过 `Normal Map` 节点转换再接 Normal 输入，否则效果错。
- ❌「三张图都必须有」—— 不。只有颜色也行，按需要加。

> **够用边界**：记住「颜色→Base Color、粗糙→Roughness、凹凸→Normal(经 Normal Map 节点)」三条接线即可。
> PBR 的光照物理原理跳过。
> **和已有认知的差异**：2D 里贴张图就是最终外观；
> 3D 里贴图是"材质的输入"，最终外观还要经过灯光和渲染计算——贴图≠最终画面。

---

<a id="c10-02"></a>

### 10.2 材质槽与 Shader Editor

**概念定义**：**材质（Material）**是附着在物体上的"表面配方"，存在**材质槽**里，可多个。
编辑材质用 **Shader Editor**（着色器编辑器），通过**节点连线**把贴图接到材质输出——
这和 ComfyUI 的节点思维很像，你会有亲切感。

**直觉类比**：像**给物体贴标签配方卡**——
材质槽是"插配方卡的卡槽"，一张卡（材质）写着"用哪几张图、怎么混合"。
Shader Editor 就是你写这张配方卡的工作台——把材料（贴图节点）用线接到成品口（Material Output）。

**界面 / 参数**：——
- **加材质**：选中物体 → 属性面板（红色球图标=材质）→ `New` 新建材质槽
- **Shader Editor**：切换工作区 `Shading`，或把某区域改成 Shader Editor
- **默认节点**：新建材质有 `Principled BSDF`（核心材质节点）+ `Material Output`（输出）
- **接线**：把贴图的 `Color` 输出连到 Principled 的对应输入（Base Color 等）
- `Principled BSDF` 是万能材质节点，绝大多数情况只用它就够

**常见误区**：
- ❌「材质和贴图是一回事」—— 不。材质是配方（节点网络），贴图是配方的原料（图片）。
- ❌「节点连线乱接」—— 颜色接颜色口、标量接标量口；Normal 要经 Normal Map 节点。

> **够用边界**：会「新建材质 → 打开 Shader Editor → 认识 Principled BSDF → 连一张颜色图」就够起步。
> 复杂节点网络（混合/程序化）是进阶（[占位 ch17](ch17_material_advanced.md)）。
> **和已有认知的差异**：这是 Blender 里最像 ComfyUI 的部分——
> 都是节点连线。你可以把 Shader Editor 当"材质版 ComfyUI"来理解，降低陌生感。

---

<a id="c10-03"></a>

### 10.3 加载/连接贴图

**概念定义**：把图片文件读进 Blender 并接到材质节点上。最省事的方式是用 `Shader Editor` 加 `Image Texture` 节点，
选图片文件，连到 Principled BSDF 的对应输入。

**直觉类比**：像**把颜料管接到画笔**——
Image Texture 节点是颜料管（装着图片），线是导管，Principled 是画笔（把颜料涂到模型上）。
接对了，模型就上色了。

**界面 / 参数**：操作步骤——
```
① 打开 Shader Editor（Shading 工作区）
② 选中 Principled BSDF 节点
③ Shift+A → 搜索 Image Texture → 添加节点
④ 节点上点 Open → 选你的贴图文件（png/jpg）
⑤ 从 Image Texture 的 Color 输出拖线 → 连到 Principled 的 Base Color
⑥ 在 Material Preview 着色模式下看效果
```
- 粗糙度图：同理加 Image Texture，连到 `Roughness`（若图是彩色的，可能要经 RGB to BW 或直接取其某通道）
- 法线图：加 Image Texture → 接到 **Normal Map 节点** → 再接 Principled 的 `Normal`

**常见误区**：
- ❌「连了线但没变化」—— 可能处于 `Solid` 着色模式，切到 `Material Preview` 才看得到材质。
- ❌「贴图文件路径丢了」—— 移动 .blend 前用 `File > External Data > Pack Resources` 把图打包进文件。
- ❌「颜色图接到了 Normal」—— 接口要对，Normal 必须经 Normal Map 节点。

> **够用边界**：会「加 Image Texture → Open 图 → Color 接 Base Color」这条最常用流程即可。
> **和已有认知的差异**：2D 里打开图片就显示；
> 3D 里图片要"接进材质节点"才生效，还要切到材质预览模式看——多了几步。

---

<a id="c10-04"></a>

### 10.4 AI 模型自带材质怎么处理

**概念定义**：有些图生 3D 方案（如带纹理的）导出的 glb **自带材质和贴图**，导入 Blender 后直接就有颜色；
有些只出白模（纯几何）要自己加。先判断属于哪种，再决定做不做材质。

**直觉类比**：像**买来的模型有的是上好色的成品，有的是待上色的白坯**——
成品（自带贴图）直接用、别乱改；白坯（白模）才需要你自己上色（加材质）。

**界面 / 参数**：判断与处理——
- **判断**：导入后切 `Material Preview`，有颜色/花纹 = 自带材质；全灰白 = 白模
- **自带材质**：通常导入 glb 时贴图已自动接好；检查是否正常，贴图丢失就重新指定路径（见 10.3）
- **白模**：
  - 简单：新建一个材质，改 Base Color 为纯色就能看（ch10 实操）
  - 进阶：找/画贴图，按 10.3 接上（需[UV](ch09_uv.md)）
- **贴图丢失（粉红/白）**：重新指定贴图文件，或 glb 内嵌贴图应能自动恢复（[ch04 4.3](../../01_comfyui_3d/docs/ch04_formats.md#c04-03)）

**常见误区**：
- ❌「自带材质一定完美」—— 有时贴图路径错、或生成质量一般，仍需检查调整。
- ❌「白模=失败」—— 白模是很多方案正常输出，补材质是后处理的一环，见 [ch05 5.1](../../01_comfyui_3d/docs/ch05_handoff.md#c05-01)。

> **够用边界**：记住「先看有没有自带材质 → 有就检查、没有就加；白模不是失败」。
> **和已有认知的差异**：这是"够用导向"again——
> 不强行给每个模型做复杂材质，按模型现状和用途决定投入多少。

---

## 小结

- PBR 三张图：Base Color（颜色）、Roughness（粗糙度）、Normal（凹凸，经 Normal Map 节点）。
- 材质=配方（节点网络），贴图=原料（图片）；Shader Editor 像"材质版 ComfyUI"，节点连线。
- 最常用流程：加 Image Texture → Open 图 → Color 接 Base Color → 切 Material Preview 看。
- 先判断模型是否自带材质：有就检查，白模再补；白模≠失败。

## 实操与下一步

- 给模型加一个基础材质：[`ch10_task.md`](../tasks/ch10_task.md)
- 下一章：[第 11 章 导出模型](ch11_export.md)
