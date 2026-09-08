> 🌐 本文档由 [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) 翻译,英文原版见原项目。

# 使用 uv 原生命令管理 Python 与软件包

本教程是 [README.md](./README.md) 中 *方案一:使用 uv* 的替代方案,面向更喜欢 `uv` 原生命令而非 `uv pip` 接口的读者。虽然 `uv pip` 已经比纯 `pip` 快,但 `uv` 的原生接口比 `uv pip` 还要快,因为它开销更小,而且不需要兼容 PyPy 软件包依赖管理等历史遗留特性。

下表对比了不同依赖与软件包管理方式的速度。这里的速度对比特指安装过程中的依赖解析速度,而不是安装后软件包的运行时性能。注意,软件包安装对本项目来说是一次性的操作,所以完全可以按整体易用性来选择方案,不必只盯着安装速度。


| 命令                  | 速度对比 |
|-----------------------|-----------------|
| `conda install <pkg>` | 最慢(基准) |
| `pip install <pkg>`   | 比上一行快 2-10× |
| `uv pip install <pkg>`| 比上一行快 5-10× |
| `uv add <pkg>`        | 比上一行快 2-5× |

本教程聚焦 `uv add`。


除此之外,本教程与 [README.md](./README.md) 中的 *方案一:使用 uv* 类似,会带你用 `uv` 完成 Python 环境搭建和软件包安装。

本教程在 macOS 电脑上演示,但在 Linux 上的流程基本相同,其他操作系统大概率也适用。


&nbsp;
## 1. 安装 uv

根据操作系统,按如下方式安装 uv。

<br>

**macOS 和 Linux**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

或者

```bash
wget -qO- https://astral.sh/uv/install.sh | sh
```

<br>

**Windows**

```bash
powershell -c "irm https://astral.sh/uv/install.ps1 | more"
```

&nbsp;

> **注意:**
> 更多安装方式请参考官方 [uv 文档](https://docs.astral.sh/uv/getting-started/installation/#standalone-installer)。

&nbsp;
## 2. 安装 Python 软件包与依赖

要从 `pyproject.toml` 文件(比如本 GitHub 仓库顶层的那份)安装全部所需软件包,在终端会话所在目录与该文件相同的前提下,运行以下命令:

```bash
uv sync --dev --python 3.11
```

> **注意:**
> 如果你的系统上没有 Python 3.11,uv 会自动帮你下载并安装。
> 建议使用比最新发布版本旧 1-3 个版本的 Python,以保证与 PyTorch 兼容。例如,最新版本是 Python 3.13 时,推荐使用 3.10、3.11 或 3.12。最新 Python 版本可以在 [python.org](https://www.python.org/downloads/) 查询。

> **注意:**
> 如果因为某些依赖(比如在 Windows 上)导致上述命令出问题,随时可以退回普通 pip:
> `uv add pip`
> `uv run python -m pip install -U -r requirements.txt`


注意,上面的 `uv sync` 命令会通过 `.venv` 子文件夹创建一个独立的虚拟环境。(如果你想删掉虚拟环境从头再来,直接删除 `.venv` 文件夹即可。)

你可以用 `uv add` 安装 `pyproject.toml` 中未指定的软件包,例如:

```bash
uv add packaging
```

也可以用 `uv remove` 移除软件包,例如:

```bash
uv remove packaging
```



&nbsp;
## 3. 运行 Python 代码

<br>

此时你的环境应该已经可以运行仓库中的代码了。

可选操作:运行仓库中的 `python_environment_check.py` 脚本来检查环境:

```bash
uv run python setup/02_installing-python-libraries/python_environment_check.py
```



<img src="https://sebastianraschka.com/images/LLMs-from-scratch-images/setup/uv-setup/uv-run-check.png?1" width="700" height="auto" alt="Uv install">


<br>

**启动 JupyterLab**

你可以通过以下命令启动 JupyterLab:

```bash
uv run jupyter lab
```

**省略 `uv run` 前缀**

如果觉得每次输入 `uv run` 麻烦,可以按下面的方式手动激活虚拟环境。

macOS/Linux:

```bash
source .venv/bin/activate
```

Windows(PowerShell):

```bash
.venv\Scripts\activate
```

然后就可以用以下命令运行脚本:

```bash
python script.py
```

并用以下命令启动 JupyterLab:

```bash
jupyter lab
```

&nbsp;
> **注意:**
> 如果 `jupyter lab` 命令出问题,也可以用虚拟环境内的完整路径启动。例如 Linux/macOS 上用 `.venv/bin/jupyter lab`,Windows 上用 `.venv\Scripts\jupyter-lab`。

&nbsp;


&nbsp;

## 可选:手动管理虚拟环境

你也可以继续用 `uv pip install` 直接从仓库安装依赖。但要注意,这种方式不会像 `uv add` 那样把依赖记录到 `uv.lock` 文件中,而且需要你手动创建并激活虚拟环境:

<br>

**1. 新建虚拟环境**

运行以下命令手动创建新的虚拟环境,它会被保存到新的 `.venv` 子文件夹中:

```bash
uv venv --python=python3.10
```

<br>

**2. 激活虚拟环境**

接下来需要激活这个新虚拟环境。

macOS/Linux:

```bash
source .venv/bin/activate
```

Windows(PowerShell):

```bash
.venv\Scripts\activate
```

<br>

**3. 安装依赖**

最后,使用 `uv pip` 接口从远程安装依赖:

```bash
uv pip install -U -r https://raw.githubusercontent.com/rasbt/LLMs-from-scratch/refs/heads/main/requirements.txt
```



---

有任何疑问?欢迎到[讨论区](https://github.com/rasbt/LLMs-from-scratch/discussions)提问。
