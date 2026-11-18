---
tags:
  - "#course/Blender"
  - "#type/练习"
  - "#topic/工作流"
created: 2026-11-18
---
# 实操 05：走一遍最小后处理链路

> 对应章节：[第 5 章 衔接 Blender](../docs/ch05_handoff.md) ｜ 预计耗时：60 分钟
> 状态：`[已完成]`

## 目标

把 ch02/ch03 生成的模型导入 Blender，走一遍最小后处理链路，导出一个"可用成品"。
**这是第 1 篇到第 2 篇的过渡任务：用到哪章查哪章，边做边学。**

## 前提

- [ ] 有一个导出的 glb 模型（[ch04](../docs/ch04_formats.md)）
- [ ] Blender 已安装（[ch01_task](ch01_task.md)）
- [ ] 零基础可先扫一眼 [ch06 界面与视图](../../02_blender_basics/docs/ch06_ui_navigation.md) 的导航三件套

## 步骤

1. **导入**：打开 Blender → 删掉默认立方体 → `File > Import > glTF 2.0` → 选你的 glb。
   按 `Home` 框选全部找到模型（见 [ch07](../../02_blender_basics/docs/ch07_import.md)）。
   - 能看到吗？____ ｜ 大小合适吗？____

2. **初步检查**：从不同角度看（鼠标中键拖动旋转），记录发现的问题：
   - 破面/洞：____ ｜ 朝向：____ ｜ 贴图在吗？____

3. **重算法线**：进入 `Edit Mode`（Tab），全选（A），`Shift+N` 重算法线（见 [ch08 8.2](../../02_blender_basics/docs/ch08_mesh_cleanup.md#c08-02)）。
   观察模型是否从"发黑"变正常。

4. **（需要时）修面/减面**：有明显破面或面数过高，按 [ch08](../../02_blender_basics/docs/ch08_mesh_cleanup.md) 处理。
   - 处理前 ____ 面 → 处理后 ____ 面

5. **（需要时）补材质**：如果是白模，按 [ch10 材质](../../02_blender_basics/docs/ch10_materials.md) 加一个基础材质。

6. **导出成品**：`File > Export > glTF 2.0`，另存为一个新文件名（保留原始 glb），
   按最终用途选设置（见 [ch11](../../02_blender_basics/docs/ch11_export.md)）。

7. **（可选）渲染一张图**：按 [ch12 渲染](../../02_blender_basics/docs/ch12_render.md) 出一张展示图。

## 验收标准

- [ ] 模型成功导入并在 Blender 里找到
- [ ] 至少做了"重算法线"一步并观察到变化
- [ ] 导出了一份"成品"文件（另存，未覆盖原始模型）
- [ ] 记录了处理前后发现/解决的问题

## 改一改会怎样（小实验）

| 改动 | 预期现象 | 为什么 |
|---|---|---|
| 导入后不删默认立方体 | 导出时多出个立方体 | 默认场景物体会混进来，见 ch05 5.2 |
| 法线反的模型不修直接渲染 | 发黑/内外颠倒 | 法线决定受光，见 ch08 |
| 覆盖原始 glb | 无法回退重修 | 保留原件是好习惯，见 ch05 5.4 |

## 可复现记录

| 项 | 值 |
|---|---|
| 源文件 / 成品文件 | |
| 导入发现的问题 | |
| 做的处理步骤 | 重算法线 / 修面 / 减面 / 补材质 |
| 面数变化 | ____ → ____ |
| 最终用途/格式 | |

## 常见问题

- 导入看不见 → 按 Home，或检查是不是太小/太远，见 [ch07](../../02_blender_basics/docs/ch07_import.md)
- 模型发黑 → 重算法线 Shift+N，见 [ch08](../../02_blender_basics/docs/ch08_mesh_cleanup.md)
- 不知道某步怎么操作 → 直接点对应章节的超链，按需查
- 其它 → [附录 C 故障排查](../../90_appendix/docs/appC_troubleshooting.md)

## 下一步

**第 1 篇 ComfyUI 3D 建模完成！** 你现在会生成 3D、导出格式、并走通 Blender 后处理。
想系统补 Blender 基础，进入 [第 2 篇](../../02_blender_basics/README.md)；
用到哪章查哪章即可，不必线性全读。
