# init.md
## 编程指导原则

### 核心规则
1. 每个代码文件顶部必须用注释标注路径：`# {relative_path}`
2. 优先修改现有文件而非创建新文件
3. 所有文件操作必须在项目目录内
4. 危险命令需要用户确认
5. 遵循aacode的编程规范和最佳实践

### 工作流程
1. 先分析需求，制定详细计划
2. 小步快跑，频繁测试验证
3. 编写自包含的测试函数
4. 使用工具前检查安全性
5. 优先使用现有程序，如需开发新程序需先检查是否已有类似功能

### 代码质量
- 遵循PEP 8/Python最佳实践
- 函数尽量不超过60行，保持单一职责
- 添加必要的文档字符串和类型注解
- 错误处理要优雅，提供有意义的错误信息
- 代码要有良好的可读性和可维护性

## Auto-DiffSynth-Studio项目说明

### 项目目的
Auto-DiffSynth-Studio是一款基于aacode和DiffSynth-Studio的图片和视频创作的Agent，整体基调是基于编程的方式去实现。通过预置项目init.md和其他文件的方式达到引导AI Agent高效完成AIGC领域工作的目的。

### 核心思想
**编程即万物** - CLI Coding Agent可以自主完成多数编程任务，因此也可以完成其他专有领域的多数任务和工作。Auto-DiffSynth-Studio是aacode在图片和视频AIGC领域的一个实例

### 支持的功能
- **图片生成** - FLUX、Qwen-Image、Z-Image、LTX-2等多种模型支持
- **图片编辑** - 图像重绘、局部编辑、风格迁移等
- **视频生成** - Wan视频生成、LTX-2音视频等
- **模型训练** - LoRA训练、ControlNet训练、蒸馏训练等
- **结构控制** - Canny、Depth、Pose等多种控制方式


## 项目结构与工作流程

### 目录结构说明

```
my_diffsynth_studio/                 # 用户工作目录（唯一工作目录）
├── .aacode/                         # Agent运行日志和上下文
├── init.md                          # 项目初始化配置（本文件）
├── outputs/                         # 生成的结果文件
│   └── <任务名称>_<日期>_<序号>/       # 任务输出目录(序号是时分，比如1330)
├── programs/                        # 预置程序目录（Agent可参考和优化）
├── resources/                       # 资源文件目录（图片、数据集等）
└── DiffSynth-Studio/                # DiffSynth-Studio源码和文档
    ├── diffsynth/                   # 核心代码
    ├── docs/                        # 文档
    │   ├── zh/                      # 中文文档
    │   │   ├── README.md            # 中文文档首页
    │   │   ├── Model_Details/       # 模型详解
    │   │   ├── Pipeline_Usage/      # 使用指南
    │   │   ├── Training/            # 训练教程
    │   │   └── Developer_Guide/    # 开发指南
    │   └── en/                      # 英文文档
    └── README.md
```

### 资源路径速查

| 资源类型 | 路径 |
|---------|------|
| DiffSynth-Studio中文文档 | `my_diffsynth_studio/DiffSynth-Studio/docs/zh/README.md` |
| DiffSynth-Studio英文文档 | `my_diffsynth_studio/DiffSynth-Studio/docs/en/README.md` |
| FLUX模型文档 | `my_diffsynth_studio/DiffSynth-Studio/docs/zh/Model_Details/FLUX.md` |
| Qwen-Image模型文档 | `my_diffsynth_studio/DiffSynth-Studio/docs/zh/Model_Details/Qwen-Image.md` |
| Z-Image模型文档 | `my_diffsynth_studio/DiffSynth-Studio/docs/zh/Model_Details/Z-Image.md` |
| Wan视频模型文档 | `my_diffsynth_studio/DiffSynth-Studio/docs/zh/Model_Details/Wan.md` |
| LTX-2模型文档 | `my_diffsynth_studio/DiffSynth-Studio/docs/zh/Model_Details/LTX-2.md` |
| 模型训练文档 | `my_diffsynth_studio/DiffSynth-Studio/docs/zh/Pipeline_Usage/Model_Training.md` |
| 显存管理文档 | `my_diffsynth_studio/DiffSynth-Studio/docs/zh/Pipeline_Usage/VRAM_management.md` |



## 产出要求

### 产出目录规范
- **根目录**: `my_diffsynth_studio/outputs/`
- **任务目录**: `outputs/<任务名称>_<日期>_<序号>/`
  - 例如: `outputs/image_generation_20260223_1200/`
  - 例如: `outputs/lora_training_20260223_1330/`
- **子目录建议**:
  - `images/` - 生成的图片
  - `videos/` - 生成的视频
  - `models/` - 训练的模型权重
  - `datasets/` - 处理的数据集
  - `logs/` - 训练日志

### 产出文件命名规范
- 图片: `<描述>_<序号>.<格式>`，如 `city_night_001.png`
- 视频: `<描述>_<日期>.<格式>`，如 `anime_video_20260223.mp4`
- 模型: `<类型>_<名称>_<日期>`，如 `lora_anime_style_20260223`

### 产出效果要求
- **图片分辨率**: 默认1024x1024，可根据需求调整
- **输出格式**: PNG (图片)、MP4 (视频)
- **质量标准**: 清晰、无明显噪点、符合描述
- **模型训练**: 保存完整权重和配置文件，便于后续使用

### 效果测试
- 对于产出的内容，可使用视觉模型工具，评估生成结果
- 如果效果不好，做相应的调整（程序、参数等）

### AIGC任务工作流程

1. **分析需求** - 理解任务目标，确定需要的模型和能力
2. **查看文档** - 参考DiffSynth-Studio文档，选择合适的模型，采用合适的方案
3. **编写程序** - 在programs目录创建或修改生成脚本
4. **执行生成** - 运行脚本生成图片/视频
5. **效果测试** - 使用视觉模型评估生成结果
6. **优化调整** - 根据评估结果调整参数或重新生成

### resources目录说明
- resources目录用于存放训练数据、参考图片等资源文件
- 需要有下级目录，并对下级目录和文件的命名进行规范

### programs目录说明
- programs目录用于存放可复用的生成脚本、测试脚本等
- 程序对DiffSynth-Studio的调用，请直接 “from DiffSynth-Studio.xx.xx import xx” 的方式进行
- Agent可将常用流程沉淀至此，便于后续复用
- 适当地对程序进行优化，以便得到更好的效果，必要的时候，你甚至可以对DiffSynth-Studio源码做相应的小优化


## init.md版本
**最后更新**: 2026-02-23
**版本**: 1.0.0
