<div align="center">

# LLMs-from-scratch 中文翻译版

**[中文版] LLMs-from-scratch — 用 PyTorch 从零开始一步步实现类 ChatGPT 的大语言模型**

[![原项目](https://img.shields.io/badge/原项目-rasbt--LLMs-from-scratch-blue?style=flat-square&logo=github)](https://github.com/rasbt/LLMs-from-scratch)
[![中文文档](https://img.shields.io/badge/中文文档-README.zh--CN.md-orange?style=flat-square)](README.zh-CN.md)
[![GitHub Stars](https://img.shields.io/github/stars/rasbt/LLMs-from-scratch?style=flat-square&label=原项目Stars)](https://github.com/rasbt/LLMs-from-scratch/stargazers)
[![微信联系](https://img.shields.io/badge/微信-uaycar-brightgreen?style=flat-square&logo=wechat)](#)

</div>

---

> 这是 [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) 的中文翻译版本。
> 完整源代码请访问原项目:https://github.com/rasbt/LLMs-from-scratch

**代部署 / 定制服务 / 技术咨询 请添加微信:uaycar**

---

## 📖 项目简介

这是 Sebastian Raschka 开源项目 LLMs-from-scratch 的中文翻译介绍仓库。原项目为图书《Build a Large Language Model (From Scratch)》(Manning, 2024)的官方代码库,不依赖任何外部 LLM 库,用纯 PyTorch 从分词器、注意力机制开始,一步步开发、预训练并微调出一个类 ChatGPT 的 GPT 模型,是理解大语言模型内部工作原理最经典的实战教程之一。本仓库提供中文导读文档,完整代码与最新更新请以原项目为准。

## ✨ 主要特性

- 从零实现 BPE 分词器,理解文本如何变成模型输入
- 手写注意力机制:从简单注意力到因果注意力、多头注意力
- 不借助任何外部 LLM 库,用纯 PyTorch 搭建完整 GPT 模型
- 在无标注文本数据上完成预训练训练循环
- 支持加载 GPT-2 等更大规模模型的官方预训练权重并继续微调
- 监督微调完成文本分类(垃圾短信识别)任务
- 指令微调让模型学会遵循指令,像 ChatGPT 一样对话
- 附加内容覆盖 KV Cache、GQA/MLA/SWA、MoE、Llama 3.2/Qwen3/Gemma 3 从零实现、DPO 偏好对齐、LoRA 高效微调等进阶专题

## 📁 文件说明

| 文件 | 说明 |
|:-----|:-----|
| README.md | 本文件(中文简介) |
| README.zh-CN.md | 详细中文文档(完整汉化) |

## 🚀 快速开始

1. 克隆原项目仓库(官方推荐浅克隆):

```bash
git clone --depth 1 https://github.com/rasbt/LLMs-from-scratch.git
```

2. 环境安装细节建议先阅读原项目 setup 目录下的 setup/README.md;

3. 按本机平台 / CUDA 版本安装 PyTorch(以 pytorch.org 官网命令为准):

```bash
pip install torch
```

4. 安装书中用到的 Python 依赖包:

```bash
pip install -r requirements.txt
```

5. 启动 Jupyter,按 ch02 → ch07 顺序逐章运行主线 Notebook:

```bash
jupyter lab
```

6. 硬件要求:主章节代码面向常规笔记本电脑设计,无需专用显卡;检测到 GPU 时会自动使用。PyTorch 新手可先看原项目附录 A 的速成介绍。

完整源代码与最新版本请访问原项目:https://github.com/rasbt/LLMs-from-scratch

## 📞 联系方式

**代部署 / 定制服务 / 技术咨询 请添加微信:uaycar**

---

本项目为 [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) 的中文翻译版本,所有代码版权归原项目作者所有,遵循其原始许可证。

**如果觉得有用,请给原项目点个 Star!** ⭐
