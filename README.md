## README

![demo](https://github.com/WangCan1178/Detail-Matters-A-Benchmark/blob/main/Resources/demo.gif)

***

### Language

<p align="center">
    <a href = "./README.zh-CN.md">简体中文</a> | <a href = "./README.md">English</a>
</p>

### Paper

**Detail Matters: A Benchmark for Automatic Evaluation and Generation of Fine-Grained Service Documents**  
(IEEE Transactions on Services Computing)

This repository provides the source code and dataset of our benchmark for automatic evaluation and generation of fine-grained Web API service documents. The benchmark consists of three complementary parts:

1. a fine-grained dataset focused on operation- and parameter-level details;
2. an evaluation metric aligned with human judgment, **Quality of Details (QoD)**;
3. baseline performance of different generative models on the parameter-description completion task.

Source code and dataset: [https://github.com/WangCan1178/Detail-Matters-A-Benchmark](https://github.com/WangCan1178/Detail-Matters-A-Benchmark)

### Project structure

- **Dataset**: Detail-Matters-A-Benchmark dataset collected from 3,796 Web API service specifications, containing 122,434 operation-level instances and 403,106 parameter-level instances with 13 attributes.
  - `gen_data.ipynb`: data crawling, extraction, and cleaning algorithms
  - `oapi.json`: operation-level dataset
  - `params.json`: parameter-level dataset
- **Experiments**: code and results of the benchmark experiments described in the paper
  - `BART`, `GPT`, `LSTM`, `T5`, `DiffuSeq`: source code of the SFT baselines
  - `result`: results folder
    - `generate_txt`: generated outputs on the test set
    - `log`: training logs
    - `score.ipynb`: evaluation with traditional similarity-based metrics and **QoD**
- **Platform**: source code of the API parameter description automatic generation platform
- **Resources**: other resources used by the project

### Detail-Matters-A-Benchmark Dataset

- Quick download: [Baidu Netdisk](https://pan.baidu.com/s/1fsfnSJNzcPvAQjfyBKmZOA?pwd=wcan) (extraction code: `wcan`)
- Scale:
  - 3,796 service specifications
  - 122,434 operation-level instances
  - 403,106 parameter-level instances
  - 13 attributes per parameter-level instance
- Attribute description:

![image-20230802130427816](https://github.com/WangCan1178/Detail-Matters-A-Benchmark/blob/main/Resources/Deprat%E5%AD%97%E6%AE%B5.png)

### QoD Metric

We propose **Quality of Details (QoD)** to evaluate fine-grained descriptive texts in service documents from four aspects:

- **Meaningfulness**
- **Directness**
- **Conciseness**
- **Diversity**

Compared with traditional similarity-based metrics (BLEU, ROUGE-L, METEOR), QoD is more interpretable and better aligned with human judgment. Implementation and evaluation scripts are provided in `Experiments/result/score.ipynb`.

### Experiments

Baselines reported in the paper:

- **SFT baselines**: Bi-LSTM, BART, T5, GPT-2, DIFFUSeq  
  (identical input formatting: `oper_desc#name#type`)
- **Zero-shot closed-source models**: GPT-5-nano, Qwen-flash  
  (prompt template is provided in the Supplementary Material)

Data split: training / validation / test = **8 : 2 : 1**.

### API parameter description automatic generation platform

- The platform runs at: [Welcome to API parameter descriptions automatic generation platform](http://58.59.92.190:54665/)
- Usage:
  - View, edit, and manage APIs
  - Click **Generate parameter descriptions** to automatically generate descriptions for **parameters without descriptions in the `desc` column**
  - Use **Save API information** for persistent storage
  - Evaluate generated descriptions with **QoD**

### Others

- Due to size limitations, additional libraries and model checkpoints have been removed from this repository
- The backend model currently loaded by the platform is **T5**; see the paper for training settings
- The quality percentage shown on the platform is computed from the statistical results in the paper
- Our method has been successfully applied to the automatic collection and evaluation of Web API services in the National Key R&D Program of China (Grant No. 2022YFF0902703)!

![image-yingyong](https://github.com/WangCan1178/Detail-Matters-A-Benchmark/blob/main/Resources/%E7%B3%BB%E7%BB%9F%E5%BA%94%E7%94%A8.jpg)

- Statement: The research presented in this paper has been partially supported by the National Key R&D Program of China (Grant No. 2022YFF0902703), the National Natural Science Foundation of China (Grant No. 62472121), the National Natural Science Foundation of China (Grant No. 62306087), and the Special Funding Program of Shandong Taishan Scholars Project. Quan Z. Sheng's work has been partially supported by Australian Research Council (ARC) Discovery Grant DP230100233.
