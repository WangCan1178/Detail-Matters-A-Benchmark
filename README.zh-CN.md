## README

![demo](https://github.com/WangCan1178/Detail-Matters-A-Benchmark/blob/main/Resources/demo.gif)

***

### 语言

<p align="center">
    <a href = "./README.zh-CN.md">简体中文</a> | <a href = "./README.md">English</a>
</p>

### 论文

**Detail Matters: A Benchmark for Automatic Evaluation and Generation of Fine-Grained Service Documents**  
（IEEE Transactions on Services Computing）

本仓库提供细粒度 Web API 服务文档自动评估与生成基准的源代码与数据集。该基准包含三个互补部分：

1. 面向操作级与参数级细节的细粒度数据集；
2. 与人类判断对齐的评估指标 **Quality of Details（QoD）**；
3. 不同生成模型在参数描述补全任务上的基线性能。

源代码与数据集：[https://github.com/WangCan1178/Detail-Matters-A-Benchmark](https://github.com/WangCan1178/Detail-Matters-A-Benchmark)

### 项目结构

- **Dataset**：Detail-Matters-A-Benchmark 数据集，采集自 3,796 个 Web API 服务规范，包含 122,434 个操作级实例与 403,106 个参数级实例，共 13 个属性。
  - `gen_data.ipynb`：数据爬取、提取与清理算法
  - `oapi.json`：操作粒度数据集
  - `params.json`：参数粒度数据集
- **Experiments**：论文中基准实验的代码与结果
  - `BART`、`GPT`、`LSTM`、`T5`、`DiffuSeq`：SFT 基线实验源码
  - `result`：结果文件夹
    - `generate_txt`：在测试集上生成的结果文件
    - `log`：训练过程输出
    - `score.ipynb`：使用传统相似度指标与 **QoD** 进行评估的程序
- **Platform**：API 参数描述自动生成平台源码
- **Resources**：项目所用其它资源

### Detail-Matters-A-Benchmark 数据集

- 快速下载：[百度网盘](https://pan.baidu.com/s/1fsfnSJNzcPvAQjfyBKmZOA?pwd=wcan)（提取码：`wcan`）
- 规模：
  - 3,796 个服务规范
  - 122,434 个操作级实例
  - 403,106 个参数级实例
  - 每个参数级实例包含 13 个属性
- 字段说明：

![image-20230802130427816](https://github.com/WangCan1178/Detail-Matters-A-Benchmark/blob/main/Resources/Deprat%E5%AD%97%E6%AE%B5.png)

### QoD 评估指标

我们提出 **Quality of Details（QoD）**，从以下四个方面评估服务文档中的细粒度描述文本：

- **Meaningfulness（有意义性）**
- **Directness（直接性）**
- **Conciseness（简洁性）**
- **Diversity（多样性）**

相较于传统相似度指标（BLEU、ROUGE-L、METEOR），QoD 更具可解释性，并与人类判断更为一致。实现与评估脚本见 `Experiments/result/score.ipynb`。

### 实验

论文报告的基线包括：

- **SFT 基线**：Bi-LSTM、BART、T5、GPT-2、DIFFUSeq  
  （统一输入格式：`oper_desc#name#type`）
- **零样本闭源模型**：GPT-5-nano、Qwen-flash  
  （提示词模板见补充材料）

数据划分：训练集 / 验证集 / 测试集 = **8 : 2 : 1**。

### API 参数描述自动生成平台

- 平台运行于：[Welcome to API parameter descriptions automatic generation platform](http://58.59.92.190:54665/)，点击可访问
- 使用方法：
  - 查看、编辑和管理 API
  - 单击 **Generate parameter descriptions**，将自动为 **`desc` 栏没有描述的参数** 生成参数描述
  - 使用 **Save API information** 进行持久化存储
  - 使用 **QoD** 进行评估

### 其它

- 因大小限制，所需额外依赖库以及模型训练得到的 checkpoint 已从本仓库中移除
- 目前平台装载的后端模型为 **T5**，具体训练设置见论文
- 平台所显示的质量百分比基准来自论文中的统计结果
- 该方法已成功应用于国家重点研发计划（批准号：2022YFF0902703）的 Web API 服务自动采集与评估中！

![image-yingyong](https://github.com/WangCan1178/Detail-Matters-A-Benchmark/blob/main/Resources/%E7%B3%BB%E7%BB%9F%E5%BA%94%E7%94%A8.jpg)

- 声明：本文研究得到国家重点研发计划项目（资助号：2022YFF0902703）、国家自然科学基金项目（资助号：62472121）、国家自然科学基金项目（资助号：62306087）以及山东省泰山学者项目专项资助的部分支持。Quan Z. Sheng 的工作得到澳大利亚研究委员会（ARC）Discovery Grant DP230100233 的部分支持。
