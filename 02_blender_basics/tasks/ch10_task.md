---
tags:
  - "#course/Blender"
  - "#type/练习"
  - "#topic/材质"
created: 2026-11-18
---
# 实操 10：给模型加一个基础材质

> 对应章节：[第 10 章 材质与贴图入门](../docs/ch10_materials.md) ｜ 预计耗时：40 分钟
> 状态：`[已完成]`

## 目标

判断模型是否自带材质；对白模，加一个基础材质（纯色起步，有条件再贴图），看到模型从灰白变有外观。

## 前提

- [ ] 有一个模型在 Blender 里（ch07/ch08 产物）
- [ ] 会切 `Material Preview` 着色模式（视图右上角球图标）
- [ ] （贴图实验可选）准备一张贴图图片 + 模型有可用 UV（[ch09](../docs/ch09_uv.md)）

## 步骤

1. **判断自带材质**：切到 `Material Preview`，看模型有没有颜色/花纹。
   - 自带材质？____（有→检查是否正常；无→白模，继续）

2. **（白模）加纯色材质**：选中物体 → 属性面板材质标签（红球）→ `New` →
   调 `Base Color` 为任意颜色 → 在 Material Preview 看模型变色。
   - 观察到的变化：____

3. **打开 Shader Editor**：切到 `Shading` 工作区，找到 `Principled BSDF` 和 `Material Output` 节点，
   确认它们连着（Principled 的 BSDF 输出 → Material Output 的 Surface）。

4. **（可选）贴图片**：`Shift+A` → Image Texture → Open 一张贴图 →
   把 `Color` 连到 Principled 的 `Base Color` → 看模型贴图效果。
   - 贴图显示正常吗？____（若错乱，检查 [UV](../docs/ch09_uv.md)）

5. **（可选）调粗糙度**：调 Principled 的 `Roughness`（0 镜面 / 1 磨砂），看高光变化。

6. **保存打包**：`File > External Data > Pack Resources`（把外部贴图打包进 .blend，避免路径丢失）。
   保存 .blend 文件。

## 验收标准

- [ ] 能判断模型是否自带材质
- [ ] 白模成功加了材质并在 Material Preview 下看到变化
- [ ] 认识了 Principled BSDF 与 Material Output 的连接
- [ ] （可选）成功贴了一张图

## 改一改会怎样（小实验）

| 改动 | 预期现象 | 为什么 |
|---|---|---|
| 连了贴图但看不出变化 | 处于 Solid 着色模式 | 切 Material Preview，见 ch10 10.3 |
| 法线图直接接 Base Color | 外观奇怪 | 法线要经 Normal Map 节点接 Normal，见 ch10 10.1 |
| 移动 .blend 后贴图丢失 | 贴图是外链路径 | 用 Pack Resources 打包，见 ch10 10.3 |
| 自带贴图模型又新建材质 | 原贴图被覆盖 | 自带材质别乱改，见 ch10 10.4 |

## 可复现记录

| 项 | 值 |
|---|---|
| 模型自带材质？ | 有/无 |
| 加的材质类型 | 纯色 / 贴图 |
| 贴图来源 | |
| Roughness 值 | |

## 常见问题

- 看不到材质 → 切 Material Preview，见 [ch10 10.3](../docs/ch10_materials.md#c10-03)
- 节点里找不到 Principled → 新建材质时默认就有；没有就 Shift+A 搜索添加
- 贴图错乱 → UV 问题，见 [ch09](../docs/ch09_uv.md)
- 其它 → [附录 C 故障排查](../../90_appendix/docs/appC_troubleshooting.md)

## 下一步

模型外观搞定后，进入 [第 11 章 导出模型](../docs/ch11_export.md)——把处理好的模型交付出去。
