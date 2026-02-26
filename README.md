# Auto-DiffSynth-Studio - AI图片视频创作助手

[![Python Version](https://img.shields.io/badge/python-3.12+-blue.svg)](https://python.org)

> 基于aacode和DiffSynth-Studio的AI图片和视频创作Agent，通过自然语言描述即可完成AIGC领域的各类任务

## 设计思想

**编程即万物** - CLI Coding Agent可以自主完成多数编程任务，因此也可以完成其他专有领域的多数任务和工作。Auto-DiffSynth-Studio是aacode在图片和视频AIGC领域的一个实践实例。

## 核心特性

- **自然语言创作** - 通过自然语言描述任务，AI Agent自动完成图片和视频生成工作
- **DiffSynth-Studio集成** - 内置强大的DiffSynth-Studio开源模型引擎，支持多种先进的图片和视频生成模型
- **智能任务规划** - 基于ReAct架构的AI Agent能够自主分析需求、制定计划、执行任务
- **预置程序资源** - 提供丰富的示例程序和文档，Agent可参考并进一步优化
- **工作目录固定** - 所有创作活动在统一的`my_diffsynth_studio`目录下，便于管理和追踪

## 支持的功能

- **图片生成** - FLUX、Qwen-Image、Z-Image、LTX-2等多种模型支持
- **图片编辑** - 图像重绘、局部编辑、风格迁移等
- **视频生成** - Wan视频生成、LTX-2音视频等
- **模型训练** - LoRA训练、ControlNet训练、蒸馏训练等
- **结构控制** - Canny、Depth、Pose等多种控制方式

## 快速开始

### 环境要求

- Python 3.12+
- Linux/macOS (Windows部分兼容)
- GPU推荐（用于模型推理和训练）

### 安装配置

```bash
# 1. 克隆项目
git clone https://github.com/kandada/Auto-DiffSynth-Studio.git
cd Auto-DiffSynth-Studio

# 2. 安装依赖
python3 init.py
# 或手动安装
pip install -r requirements.txt

# 3. 配置API密钥
export LLM_API_KEY="your-api-key"
export LLM_API_URL="your-api-url" 
export LLM_MODEL_NAME="your-model-name"
```

### 开始使用

```bash
# 基本用法
python main_diffsynth.py "生成一张科技感的城市夜景图片"

# 规划优先模式（复杂任务推荐）
python main_diffsynth.py "训练一个LoRA模型" --plan-first

# 交互式连续对话
python main_diffsynth.py "创建一个动漫风格视频" --interactive

# 指定会话继续
python main_diffsynth.py --session session_20250128_123456_0 "继续优化视频效果"
```

> **注意**: 项目工作目录固定为`my_diffsynth_studio`，所有生成的结果保存在该目录的`outputs`子目录下。
> **资源**: 如果你有一些数据和资源，可以直接放在`my_diffsynth_studio/resources`目录下，你只需要在任务描述中简单提一下有这些资源，Agent会自动加载。

## 项目结构

```
Auto-DiffSynth-Studio/
├── core/                           # aacode核心代码
│   ├── agent.py
│   ├── main_agent.py
│   └── ...
│ 
├── tools/                          # aacode工具集
│   ├── atomic_tools.py
│   ├── code_tools.py
│   └── ...
│
├── my_diffsynth_studio/           # 用户工作目录（唯一工作目录）
│   ├── .aacode/                   # Agent运行日志和上下文
│   ├── init.md                    # 项目初始化配置
│   ├── outputs/                   # 生成的结果文件
│   ├── programs/                  # 预置程序目录
│   ├── resources/                 # 资源文件目录
│   └── DiffSynth-Studio/          # DiffSynth-Studio源码
│
├── main_diffsynth.py                         # 主程序入口
├── README_aacode.md               # aacode原始文档
└── requirements.txt               # 项目依赖
```

## 配置说明

### 大语言模型

项目支持DeepSeek、OpenAI等兼容OpenAI API的模型：

```bash
# DeepSeek
export LLM_API_KEY="your-deepseek-key"
export LLM_API_URL="https://api.deepseek.com/v1"
export LLM_MODEL_NAME="deepseek-chat"

# OpenAI
export LLM_API_KEY="your-openai-key"
export LLM_API_URL="https://api.openai.com/v1"
export LLM_MODEL_NAME="gpt-4"
```

### 多模态大模型
当前仅支持moonshot kimi-k2.5模型，请在aacode_config.yaml中配置api_key


### 搜索引擎（可选）

支持SearXNG搜索，需自行部署并配置：

```bash
# 比如：
export SEARCHXNG_URL="http://192.168.0.106:8081"
```

### DiffSynth-Studio源码
你可从github克隆最新版本至my_diffsynth_studio目录下，并在DiffSynth-Studio目录中增加__init__.py文件

### 本地模型支持
程序最好运行在搭载超过24G显存英伟达GPU的linux机器上（作者测试环境是ubuntu22.04，配套显卡是24G的4090显卡）
请安装好英伟达的驱动、CUDA和cuDNN环境

## 最佳实践

### 1. 任务描述要具体

✅ **好的描述**:
```
"使用Qwen-Image模型生成一张现代建筑的高清图片，
包含蓝天白云背景，并训练一个LoRA用于该风格"
```

❌ **不好的描述**:
```
"生成一张图片"
```

### 2. 分步骤执行复杂任务

```bash
# 第一步：了解模型
python main.py "查看DiffSynth-Studio支持哪些图片生成模型"

# 第二步：生成测试图片
python main.py "使用Z-Image模型生成一张测试图片"

# 第三步：训练LoRA
python main.py "基于生成的图片训练一个LoRA模型"
```

### 3. 利用init.md配置项目

编辑`my_diffsynth_studio/init.md`文件，添加项目特定的规则和要求：

```markdown
# 项目配置

## 生成要求
- 图片分辨率: 1024x1024
- 输出格式: PNG
- 模型优先使用: Qwen-Image

## 文件规范
- 所有Python脚本放在programs目录
- 生成图片统一保存在outputs目录
- 资源文件放在resources目录
```

## DiffSynth-Studio文档

项目内置了完整的DiffSynth-Studio文档，位于`my_diffsynth_studio/DiffSynth-Studio/docs/`：

- [中文文档](my_diffsynth_studio/DiffSynth-Studio/docs/zh/README.md)
- [English Docs](my_diffsynth_studio/DiffSynth-Studio/docs/en/README.md)

支持的模型详情请参考：
- [FLUX](my_diffsynth_studio/DiffSynth-Studio/docs/zh/Model_Details/FLUX.md)
- [Qwen-Image](my_diffsynth_studio/DiffSynth-Studio/docs/zh/Model_Details/Qwen-Image.md)
- [Z-Image](my_diffsynth_studio/DiffSynth-Studio/docs/zh/Model_Details/Z-Image.md)
- [Wan](my_diffsynth_studio/DiffSynth-Studio/docs/zh/Model_Details/Wan.md)
- [LTX-2](my_diffsynth_studio/DiffSynth-Studio/docs/zh/Model_Details/LTX-2.md)

## 架构设计

基于aacode的分层架构：

```
📁 架构层次
├── 🤖 MainAgent           # 主控制器，任务分解和协调
├── 🔄 ReActLoop           # 智能思考-行动循环
├── 📚 ContextManager      # 文件化上下文管理
├── 🛠️ AtomicTools         # 原子工具集（文件、命令、搜索）
├── 💻 CodeTools           # 代码工具集（执行、测试）
└── 🛡️ SafetyGuard         # 安全护栏系统
```

结合DiffSynth-Studio的模型能力：

```
🎨 AIGC能力
├── 🖼️ Image Generation    # 图片生成
├── ✏️ Image Editing       # 图片编辑
├── 🎬 Video Generation    # 视频生成
├── 🧠 Model Training      # 模型训练
└── 🎯 ControlNet          
```

## 了解更多

- aacode原始文档: [README_aacode.md](README_aacode.md)
- DiffSynth-Studio: [GitHub](https://github.com/modelscope/DiffSynth-Studio)

## 许可证

GPL3.0

## 联系方式

- 作者: xiefujin (github: kandada, 邮箱: 490021684@qq.com)
