# LLMs-from-scratch 中文文档

[![原项目](https://img.shields.io/badge/原项目-rasbt--LLMs-from-scratch-blue?style=flat-square&logo=github)](https://github.com/rasbt/LLMs-from-scratch)
[![原项目Stars](https://img.shields.io/github/stars/rasbt/LLMs-from-scratch?style=flat-square&label=原项目Stars)](https://github.com/rasbt/LLMs-from-scratch/stargazers)
[![微信联系](https://img.shields.io/badge/微信-uaycar-brightgreen?style=flat-square&logo=wechat)](#)

> 本文档是 [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) 的中文翻译版本,与 Sebastian Raschka 所著《Build a Large Language Model (From Scratch)》(Manning, 2024, ISBN 9781633437166)一书配套。目录与链接保持与原仓库一致,便于对照阅读;内容如与原项目有出入,以原项目为准。
>
> **代部署 / 定制服务 / 技术咨询 请添加微信:uaycar**

## 📖 项目简介

原项目是《Build a Large Language Model (From Scratch)》一书的官方代码仓库,目标是开发、预训练并微调一个类 GPT 的大语言模型。全书采用"由内而外"的讲法:不依赖任何外部 LLM 库,用 PyTorch 从零开始,一步步写出一个自己专属的、小而完整可用的大语言模型。这一构建路径与 ChatGPT 背后大规模基础模型的训练方法一脉相承,书中还提供了加载更大规模预训练模型官方权重并进行微调的代码。

## ✨ 主要特性

- 纯 PyTorch 从零实现,不借助 transformers 等现成 LLM 库;
- 完整覆盖"分词 → 注意力 → 模型搭建 → 预训练 → 微调"全链路;
- 支持加载 GPT-2 等官方预训练权重,验证自己从零写出的模型;
- 每章配套练习题与解答 Notebook,另有免费 170 页测验 PDF(Test Yourself 系列);
- 附加内容极丰富:KV Cache、GQA / MLA / SWA / MoE、Llama 3.2 / Qwen3 / Gemma 3 从零实现、GPT 转 Llama、DPO 偏好对齐、LoRA 高效微调等;
- 主章节代码面向普通笔记本电脑设计,CPU 即可在合理时间内跑通,检测到 GPU 时自动调用;
- 配套 17 小时 15 分钟视频课程,章节与图书一一对应;
- 提供专门的 setup 环境文档、troubleshooting 排错指南与活跃的 GitHub Discussions 社区。

## 🗂️ 章节总览

| 章节 | 主题(汉化) | 原仓库目录 |
|:-----|:-----|:-----|
| 环境准备 | 安装建议 / 如何阅读本书 | [setup](https://github.com/rasbt/LLMs-from-scratch/tree/main/setup) |
| 第 1 章 | 理解大语言模型(无代码) | — |
| 第 2 章 | 处理文本数据(BPE 分词) | ch02 |
| 第 3 章 | 编码注意力机制(因果注意力、多头注意力) | ch03 |
| 第 4 章 | 从零实现 GPT 模型 | ch04 |
| 第 5 章 | 在无标注数据上预训练 | ch05 |
| 第 6 章 | 文本分类微调(垃圾短信识别) | ch06 |
| 第 7 章 | 指令微调(让模型遵循指令) | ch07 |
| 附录 A | PyTorch 入门 | appendix-A |
| 附录 B | 参考文献与延伸阅读 | appendix-B |
| 附录 C | 练习题解答 | appendix-C |
| 附录 D | 给训练循环增加进阶功能(学习率调度等) | appendix-D |
| 附录 E | 基于 LoRA 的参数高效微调 | appendix-E |

代表性主线代码(保留原文件名,便于到原仓库对照):

- `ch02/01_main-chapter-code/ch02.ipynb`:文本数据处理主线;
- `ch03/01_main-chapter-code/ch03.ipynb`:注意力机制主线;
- `ch04/01_main-chapter-code/gpt.py`:GPT 模型完整实现(汇总版);
- `ch05/01_main-chapter-code/gpt_train.py`:预训练训练循环(汇总版);
- `ch06/01_main-chapter-code/gpt_class_finetune.py`:分类微调脚本;
- `ch07/01_main-chapter-code/gpt_instruction_finetuning.py`:指令微调脚本。

## 🧰 环境与使用说明

前置要求:扎实的 Python 编程基础;有深度神经网络经验更佳;不要求熟练 PyTorch——附录 A 提供速成介绍,作者另有免费教程 PyTorch in One Hour。

1. 下载仓库(官方推荐浅克隆,省时省空间):

```bash
git clone --depth 1 https://github.com/rasbt/LLMs-from-scratch.git
```

2. 环境与依赖安装的详细指引,优先阅读原仓库 setup/README.md;

3. 按本机平台 / CUDA 版本安装 PyTorch(以 pytorch.org 官网命令为准);

4. 安装书中用到的 Python 包:

```bash
pip install -r requirements.txt
```

5. 启动 Jupyter 后按章节顺序逐个运行 Notebook;遇到问题先查原仓库 troubleshooting.md,再到 GitHub Discussions 提问。

硬件要求:主章节代码面向常规笔记本电脑,不需要专用硬件;机器带 GPU 时代码会自动调用。涉及加载大模型权重或长时间训练的实验,在低配设备上耗时会更长。

## 🎁 附加内容(节选)

原仓库每章目录下有大量 bonus 材料,以下为代表性条目(标题汉化、英文名与路径保留):

- 从零实现 BPE 分词器(BPE Tokenizer From Scratch,`ch02/05_bpe-from-scratch`);
- 高效多头注意力实现对比(MHA implementations,`ch03/02_bonus_efficient-multihead-attention`);
- KV Cache、GQA、MLA、Sliding Window Attention、MoE 等注意力与架构专题(`ch04`);
- Llama 3.2 / Qwen3 / Gemma 3 等主流架构从零实现(`ch05/07_gpt_to_llama`、`ch05/11_qwen3`、`ch05/12_gemma3` 等);
- 在 Project Gutenberg 语料上预训练、训练超参调优、给预训练模型搭一个聊天界面(`ch05`);
- 在 50k IMDb 影评数据上微调不同模型做情感分类(`ch06/03_bonus_imdb-classification`);
- 用 Ollama / OpenAI API 评估指令微调效果、DPO 直接偏好优化、指令数据集生成与改进(`ch07`);
- 更多内容见原仓库 README 的 Bonus Material 一节。

## 📚 配套资源

- 视频课程:Master and Build Large Language Models(Manning,17 小时 15 分钟,作者逐章编码演示);
- 练习:每章若干练习,解答集中于附录 C,并可下载每章约 30 道测验题的免费 PDF;
- 续作:《Build A Reasoning Model (From Scratch)》——从预训练模型出发,讲解推理时扩展、强化学习(GRPO)与蒸馏等提升推理能力的方法,代码见 rasbt/reasoning-from-scratch;
- 交流:Manning Forum 与原仓库 GitHub Discussions;因代码与纸质书内容一一对应,原项目不接受扩展主章节代码的贡献。

## 📄 版权与致谢

- 原项目与图书版权归作者 Sebastian Raschka 及出版社 Manning 所有,代码遵循原项目原始许可证;学术引用格式见原 README 的 Citation 一节。
- 本仓库仅提供中文翻译文档,不含原项目任何源代码;
- 如果本翻译对你有帮助,请到原项目点一个 Star:https://github.com/rasbt/LLMs-from-scratch ⭐

**代部署 / 定制服务 / 技术咨询 请添加微信:uaycar**
