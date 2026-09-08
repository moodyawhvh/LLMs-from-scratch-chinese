> 🌐 本文档由 [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) 翻译,英文原版见原项目。

# 使用 pixi 原生命令管理 Python 与软件包

本教程是 [`./native-uv.md`](native-uv.md) 的替代方案,面向更喜欢 `pixi` 原生命令、而不想用 `conda`、`pip` 这类传统环境与软件包管理器的读者。

注意,pixi 底层使用的正是 [`./native-uv.md`](native-uv.md) 中介绍的 `uv add` 机制。

pixi 和 uv 都是现代化的 Python 软件包与环境管理工具,但 pixi 是一个多语言(polyglot)软件包管理器,不仅管理 Python 还支持其他语言(类似 conda),而 uv 是 Python 专属工具,为超高速的依赖解析和软件包安装而生。

如果你需要一个支持多语言(不只是 Python)的多语言包管理器,或者更喜欢类似 conda 的声明式环境管理方式,就可以选择 pixi 而不是 uv。更多信息请访问官方 [pixi 文档](https://pixi.sh/latest/)。

本教程在 macOS 电脑上演示,但在 Linux 上的流程基本相同,其他操作系统大概率也适用。

&nbsp;
## 1. 安装 pixi

根据操作系统,按如下方式安装 pixi。

<br>

**macOS 和 Linux**

```bash
curl -fsSL https://pixi.sh/install.sh | sh
```

或者

```bash
wget -qO- https://pixi.sh/install.sh | sh
```

<br>

**Windows**

从官方[文档](https://pixi.sh/latest/installation/#__tabbed_1_2)下载安装器,或运行文档中列出的 PowerShell 命令。



> **注意:**
> 更多安装方式请参考官方 [pixi 文档](https://pixi.sh/latest/)。


&nbsp;
## 2. 安装 Python

你可以用 pixi 安装 Python:

```bash
pixi add python=3.10
```

> **注意:**
> 建议安装比最新发布版本至少旧 2 个版本的 Python,以保证与 PyTorch 兼容。例如,最新版本是 Python 3.13 时,推荐安装 3.10 或 3.11。最新 Python 版本可以在 [python.org](https://www.python.org) 查询。

&nbsp;
## 3. 安装 Python 软件包与依赖

要从 `pixi.toml` 文件(比如本 GitHub 仓库顶层的那份)安装全部所需软件包,在终端会话所在目录与该文件相同的前提下,运行以下命令:

```bash
pixi install
```

> **注意:**
> 如果遇到依赖问题(比如在 Windows 上),随时可以退回 pip:`pixi run pip install -U -r requirements.txt`

默认情况下,`pixi install` 会为该项目创建一个专属的独立虚拟环境。

你可以用 `pixi add` 安装 `pixi.toml` 中未指定的软件包,例如:

```bash
pixi add packaging
```

也可以用 `pixi remove` 移除软件包,例如:

```bash
pixi remove packaging
```

&nbsp;
## 4. 运行 Python 代码

此时你的环境应该已经可以运行仓库中的代码了。

可选操作:运行仓库中的 `python_environment_check.py` 脚本来检查环境:

```bash
pixi run python setup/02_installing-python-libraries/python_environment_check.py
```

<br>

**启动 JupyterLab**

你可以通过以下命令启动 JupyterLab:

```bash
pixi run jupyter lab
```


---

有任何疑问?欢迎到[讨论区](https://github.com/rasbt/LLMs-from-scratch/discussions)提问。
