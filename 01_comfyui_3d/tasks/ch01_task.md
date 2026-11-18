---
tags:
  - "#course/Blender"
  - "#type/练习"
  - "#topic/3d概览"
created: 2026-11-18
---
# 实操 01：认识 3D 流程并检查环境

> 对应章节：[第 1 章 3D 生成概览](../docs/ch01_3d_overview.md) ｜ 预计耗时：30 分钟
> 状态：`[已完成]`

## 目标

建立对 3D 生成流程的整体认知，并检查自己的机器是否具备跑 ComfyUI 3D + Blender 的基本条件。
**本篇以"看懂流程、备好环境"为主，不急着生成。**

## 前提

- [ ] 已了解 ComfyUI 是什么（[主仓库 ch01](https://github.com/tliu154/ComfyUI_study_record/blob/main/00_getting_started/docs/ch01_what_is_comfyui.md)）
- [ ] ComfyUI 能启动（[主仓库 ch02](https://github.com/tliu154/ComfyUI_study_record/blob/main/00_getting_started/docs/ch02_installation.md)）

## 步骤

1. **画流程默写**：不看文档，凭记忆写出 3D 生成的五步主线（输入→?→?→?→交付），
   再对照 [ch01 1.4](../docs/ch01_3d_overview.md#c01-04) 补全。填出中间三步：
   ________ → ________ → ________

2. **检查 ComfyUI**：启动 ComfyUI，确认能打开 `localhost:8188`。
   在节点搜索框搜 `3D`、`glb`、`mesh` 等词，看当前装了哪些 3D 相关节点（大概率很少或没有）。
   - 已装的 3D 节点：____________

3. **检查显卡/显存**：记录你的显卡型号与显存大小（任务管理器 GPU 页 / `nvidia-smi`）。
   3D 生成通常比 2D 更吃显存——填表：
   - 显卡：________ ｜ 显存：________ GB

4. **安装 Blender（可跳过）**：到 https://www.blender.org/ 下载安装最新版（免费）。
   装好打开，确认能进入默认界面。**若暂时不装也行**，先看文档，等真正做后处理前再装。
   - Blender 版本：________（未装填"暂未装"）

5. **找几个 3D 模型看看**：下载或在线预览一个 `.glb` 示例模型（如 Khronos glTF Sample Models 官网），
   在支持 glb 的查看器（如 Windows 3D 查看器、Blender）里打开，转着看一圈，
   直观感受"3D 是可从任意角度看的数据体"。

## 验收标准

- [ ] 能默写并说出 3D 生成五步主线
- [ ] 记录了显卡显存，知道 3D 比 2D 更吃资源
- [ ] （可选）Blender 已装好，或明确记录"暂不装，先看文档"
- [ ] 亲眼看过一个 3D 模型的"可旋转"特性

## 改一改会怎样（小实验）

| 改动 | 预期现象 | 为什么 |
|---|---|---|
| 在 ComfyUI 搜 3D 节点但没装相关包 | 搜不到 / 很少 | 3D 功能靠自定义节点，见 ch01 1.3 |
| 用手机看 glb vs 在 3D 软件看 | 手机多为静态预览 | 3D 的价值在于可交互视角，见 ch01 1.1 |

## 可复现记录

| 项 | 值 |
|---|---|
| ComfyUI 状态 | 能启动 / 不能 |
| 已装 3D 节点 | |
| 显卡 / 显存 | |
| Blender 版本 | |

## 常见问题

- 搜不到 3D 节点 → 正常，需要装自定义节点，后面章节会讲（也可参考 [主仓库 ch24 Manager](https://github.com/tliu154/ComfyUI_study_record/blob/main/06_ecosystem/docs/ch24_manager.md)）
- Blender 下载慢 → 官网走国内镜像/社区网盘，或先跳过
- 显存很小（<4GB）→ 3D 生成可能受限，先学概念，实操时用轻量模型/云端方案

## 下一步

环境就绪后，进入 [第 2 章 图生 3D](../docs/ch02_img2img3d.md)——从一张图生成第一个 3D 模型。
