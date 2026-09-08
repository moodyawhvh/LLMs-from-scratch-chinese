> 🌐 本文档由 [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) 翻译,英文原版见原项目。

# 故障排查指南

本页面汇总了学习本书过程中常见的问题与环境配置技巧。

&nbsp;
## Notebook 图片加载问题

各章节的 Notebook 使用托管在 `https://sebastianraschka.com/images/LLMs-from-scratch-images/...` 的 Markdown 图片链接。这样做可以控制仓库的下载体积,但也意味着图片的显示依赖于图床服务和你的网络连接。

如果 `.ipynb` Notebook 中的图片无法显示:

- 直接在浏览器中打开某个图片 URL 试试,例如 [https://sebastianraschka.com/images/LLMs-from-scratch-images/ch02_compressed/02.webp](https://sebastianraschka.com/images/LLMs-from-scratch-images/ch02_compressed/02.webp)。
- 如果该 URL 在浏览器中也打不开,问题多半出在网站临时故障、DNS、VPN、代理、防火墙或本地网络,而不是 Notebook 本身。
- 建议换一台设备或另一个网络再试一次(比如用手机打开图片);如果手机上能正常加载,那大概率是你电脑上的 VPN 或防火墙问题。
- 如果手机上也加载不出来,欢迎到 GitHub 提 [Issue](https://github.com/rasbt/LLMs-from-scratch/issues),帮我进一步排查。

&nbsp;
## 更新仓库的同时保留个人 Notebook 修改

如果你想在修改 Notebook 的同时还能持续获取仓库更新,请先 fork 本仓库,再克隆你自己的 fork。书中主要 Notebook 与纸质书内容保持同步,一般不会改动(关键修复除外),仓库的大多数更新都是新增附加内容。

Notebook 文件本质上是 JSON 文件,Git 的 diff 和合并冲突往往很难阅读。为了避免不必要的冲突,建议你把自己的实验与仓库中被跟踪的书本 Notebook 分开管理:

- 修改 Notebook 前先复制一份,例如从 `ch02.ipynb` 复制为 `ch02_experiments.ipynb`。
- 把你的草稿 Notebook 放在单独的文件夹或你自己的分支上。
- 通过 `upstream` 远程仓库拉取原仓库的更新,只在确实需要时才合并或变基。

创建 fork 并克隆的步骤:

1. 打开 [https://github.com/rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)。
2. 点击 GitHub 页面右上角的 **Fork** 按钮。
3. 克隆你的 fork,把 `YOUR-USERNAME` 替换成你的 GitHub 用户名:

```bash
git clone https://github.com/YOUR-USERNAME/LLMs-from-scratch.git
cd LLMs-from-scratch
```

然后把原仓库添加为 `upstream`,以便将来获取更新:

```bash
git remote add upstream https://github.com/rasbt/LLMs-from-scratch.git
git fetch upstream
git merge upstream/main
```

如果确实需要合并你改过的 Notebook,可以考虑安装 [`nbdime`](https://nbdime.readthedocs.io/),它提供针对 Notebook 的 diff 和合并工具:

```bash
pip install nbdime
nbdime config-git --enable
```

更多背景信息参见 [#1015](https://github.com/rasbt/LLMs-from-scratch/issues/1015)。

&nbsp;
## Apple Silicon 与 MPS 支持

部分 Notebook 和脚本只在检测到 `cuda` 时使用 GPU,否则回退到 `cpu`,并不会选择 Apple 的 `mps` 后端。很多地方刻意不启用 `mps` 支持,因为早期版本的 PyTorch/MPS 在若干示例中会产生不稳定或不一致的结果,训练和微调场景尤其明显。

如果你在 Apple Silicon Mac 上看到损失曲线发散、损失剧烈跳变、生成文本质量差,或结果与书中不符,请先在 `cpu` 上重新运行该示例。如果想要更快的训练速度且结果与书一致,建议使用本地 NVIDIA GPU 的 `cuda`,或云 GPU。

更新版本的 PyTorch 可能会改善 MPS 的表现,你可以在仔细验证结果的前提下在本地尝试 `mps`。不过,如果你自己给脚本添加 `mps` 支持,请注意 `pin_memory=True`、`torch.compile` 以及 DDP/多 GPU 代码等 CUDA 专属选项可能需要单独加保护逻辑。

更多背景信息参见 [#977](https://github.com/rasbt/LLMs-from-scratch/issues/977)、[#625](https://github.com/rasbt/LLMs-from-scratch/discussions/625)、[#644](https://github.com/rasbt/LLMs-from-scratch/discussions/644)、[#442](https://github.com/rasbt/LLMs-from-scratch/discussions/442) 和 [#846](https://github.com/rasbt/LLMs-from-scratch/issues/846)。

&nbsp;
## 其他问题

遇到其他问题,欢迎到 GitHub 提交新的 [Issue](https://github.com/rasbt/LLMs-from-scratch/issues)。
