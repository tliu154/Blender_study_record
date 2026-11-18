---
tags:
  - "#course/Blender"
  - "#type/笔记"
  - "#topic/排错"
  - "#source/官方文档"
created: 2026-11-18
---
# 附录 C 故障排查（Troubleshooting）

> 前置：无，报错时按现象查 ｜ 状态：`[已完成]` ｜ 所属：`90_appendix/`

**一句话**：把「ComfyUI 生成 3D → 导入 Blender → 后处理 → 导出/渲染」这条线上常见毛病，
按「**现象 → 原因 → 处理**」列成速查条。Ctrl+F 搜关键词（看不见、发黑、白模、粉红…）快速定位。

> 排查心法：一次只改一处，改完重试，才能定位真因。

## 目录

| 阶段 | 现象 |
|---|---|
| ComfyUI 生成 | [搜不到 3D 节点 / 显存爆 / 结果不像](#appC-01) |
| 导入 Blender | [看不见模型 / 导入失败 / 白模](#appC-02) |
| 检查/网格 | [模型发黑 / 法线反 / 破面](#appC-03) |
| UV/材质 | [贴图错乱 / 白模 / 粉红](#appC-04) |
| 导出 | [朝向错 / 尺度错 / 修改器没生效](#appC-05) |
| 渲染 | [全黑 / 有噪点 / 没保存](#appC-06) |

---

<a id="appC-01"></a>

### 阶段一：ComfyUI 生成 3D 的问题

| 现象 | 原因 | 处理 |
|---|---|---|
| 搜不到 3D 节点 | 没装 3D 自定义节点包 | 用 Manager 装对应节点包 + 模型，重启（[主仓库 ch24](https://github.com/tliu154/ComfyUI_study_record/blob/main/06_ecosystem/docs/ch24_manager.md)）|
| 显存爆（OOM）| 3D 生成很吃显存 | 换轻量方案（TripoSR）、降面数/质量档（[ch02 2.2](../../01_comfyui_3d/docs/ch02_img2img3d.md#c02-02)）|
| 生成结果不像输入图 | 输入图质量差 / 背面靠猜 | 换"主体单一+背景干净+正视角"的图（[ch02 2.4](../../01_comfyui_3d/docs/ch02_img2img3d.md#c02-04)）|
| 文生 3D 太随机 | 没参考约束 | 走"文生图→图生3D"路线（[ch03 3.3](../../01_comfyui_3d/docs/ch03_text2_3d.md#c03-03)）|

---

<a id="appC-02"></a>

### 阶段二：导入 Blender 的问题

| 现象 | 原因 | 处理 |
|---|---|---|
| 导入后看不见模型 | 太小/太远/在视野外 | 按 `Home`；看大纲点名字；`S` 放大（[ch07 7.4](../../02_blender_basics/docs/ch07_import.md#c07-04)）|
| 导入失败/报错 | 文件损坏或格式不对 | 换已知能用的 glb 测试；确认是 glb/obj 支持格式 |
| 场景多出个立方体 | 没删默认 Cube | 导入前删默认物体（[ch07 7.1](../../02_blender_basics/docs/ch07_import.md#c07-01)）|
| 导入 obj 是白模 | 贴图文件没一起带 | obj/.mtl/图片放一起（[ch04 4.3](../../01_comfyui_3d/docs/ch04_formats.md#c04-03)）|

---

<a id="appC-03"></a>

### 阶段三：检查与网格问题

| 现象 | 原因 | 处理 |
|---|---|---|
| 模型发黑 | 法线反了 | 编辑模式全选 → `Shift+N` 重算法线（[ch08 8.2](../../02_blender_basics/docs/ch08_mesh_cleanup.md#c08-02)）|
| Face Orientation 红色多 | 面朝内 | 同上重算法线；仍有红色可能要补破面（[ch08 8.3](../../02_blender_basics/docs/ch08_mesh_cleanup.md#c08-03)）|
| 有洞/打印失败 | 破面、非流形、非水密 | 补洞 `F`、合并顶点、修封闭（[ch08](../../02_blender_basics/docs/ch08_mesh_cleanup.md)）|
| 面数太高、卡顿 | AI 网格过密 | Decimate 减面，Ratio 从 0.5 试（[ch08 8.3](../../02_blender_basics/docs/ch08_mesh_cleanup.md#c08-03)）|
| 平滑后棱角糊了 | 过度平滑 | 用 Weighted Normal 保留硬边（[ch08 8.4](../../02_blender_basics/docs/ch08_mesh_cleanup.md#c08-04)）|

---

<a id="appC-04"></a>

### 阶段四：UV 与材质问题

| 现象 | 原因 | 处理 |
|---|---|---|
| 贴图错乱/拉伸 | UV 乱或缺失 | 检查 UV，必要时 Smart UV Project 重展（[ch09 9.3](../../02_blender_basics/docs/ch09_uv.md#c09-03)）|
| 白模（全灰白）| 模型无材质 或 处于 Solid 着色 | 切 Material Preview；白模则加材质（[ch10](../../02_blender_basics/docs/ch10_materials.md)）|
| 粉红色 | 贴图丢失/路径错 | 重新指定贴图，或 Pack Resources；glb 内嵌应可恢复（[ch10 10.3](../../02_blender_basics/docs/ch10_materials.md#c10-03)）|
| 连了贴图没变化 | 在 Solid 着色模式 | 切 Material Preview（[ch10 10.3](../../02_blender_basics/docs/ch10_materials.md#c10-03)）|
| 法线图效果奇怪 | 法线图直接接了颜色口 | 经 Normal Map 节点再接 Normal（[ch10 10.1](../../02_blender_basics/docs/ch10_materials.md#c10-01)）|

---

<a id="appC-05"></a>

### 阶段五：导出问题

| 现象 | 原因 | 处理 |
|---|---|---|
| 到引擎朝向错（躺着/倒着）| Up 轴不一致 | 导出设 +Y Up（[ch11 11.2](../../02_blender_basics/docs/ch11_export.md#c11-02)）|
| 尺度巨大/极小 | 没 Apply Scale | `Ctrl+A` → Scale 后重导（[ch11 11.1](../../02_blender_basics/docs/ch11_export.md#c11-01)）|
| 减面/处理没体现在导出里 | 没勾 Apply Modifiers | 导出时勾选（[ch11 11.4](../../02_blender_basics/docs/ch11_export.md#c11-04)）|
| 导出白模 | 贴图没带上 | glb 勾贴图/内嵌；obj 连贴图一起给（[ch11 11.4](../../02_blender_basics/docs/ch11_export.md#c11-04)）|
| 成品里多出杂物 | 全选导出了辅助物体 | 只选目标物体导出（[ch11 11.1](../../02_blender_basics/docs/ch11_export.md#c11-01)）|

---

<a id="appC-06"></a>

### 阶段六：渲染问题

| 现象 | 原因 | 处理 |
|---|---|---|
| 渲染全黑 | 没灯光/世界太暗/相机被挡 | 加面光、调世界强度、检查相机（[ch12 12.2](../../02_blender_basics/docs/ch12_render.md#c12-02)）|
| 报错没相机 | 场景没 Camera | `Shift+A` → Camera（[ch12 12.1](../../02_blender_basics/docs/ch12_render.md#c12-01)）|
| Cycles 有噪点 | 采样不足 | 加采样 / 开降噪（[ch12 12.3](../../02_blender_basics/docs/ch12_render.md#c12-03)）|
| 渲染完没图 | 没手动保存 | 渲染窗口 `Image > Save As`（[ch12 12.4](../../02_blender_basics/docs/ch12_render.md#c12-04)）|
| 过曝/死黑 | 灯光过强/不足 | 调 Energy 和世界强度（[ch12 12.2](../../02_blender_basics/docs/ch12_render.md#c12-02)）|

---

## 小结

- 按阶段对号入座：生成 → 导入 → 网格 → UV/材质 → 导出 → 渲染。
- 高频三件套：看不见（`Home`）、发黑（`Shift+N` 重算法线）、白模/粉红（贴图问题）。
- 一次只改一处，改完验证。

> 回 [附录首页](../README.md) ｜ 回 [仓库首页](../../README.md)
