# 思想
编程即万物，CLI coding Agent可自主完成多数编程任务，因此也可以完成其他专有领域的多数任务和工作。Auto-DiffSynth-Studio是aacode在图片和视频AIGC领域的一个实例。


# 思路定位
* Auto-DiffSynth-Studio是一款基于aacode和DiffSynth-Studio的图片和视频创作的Agent，整体基调是基于编程的方式去实现。通过预置项目init.md和其他文件的方式达到引导AI Agent高效完成AIGC领域工作的目的。
* 主要是在init.md里面集成一些要求，提供一些资源入口，还有产出期望。
* 做一个定制的“main_diffsynth.py”（原有的main.py不做修改），在原有main基础上相应优化，做相应的任务定制，包括定死工作目录，及描述一些产出标准。
* 一些外部资源，引导用户写到init.md文档中（初始化也要写一些进去，尤其对于DiffSynth-Studio的一些实用教程）



# 项目结构一栏
Auto-DiffSynth-Studio/
├── core/                           # aacode源代码--不变
│   ├── agent.py
│   ├── main_agent.py
│   └── ...                         # 其他文件
│ 
├── tools/                           # aacode源代码--不变
│   ├── atomic_tools.py
│   ├── code_tools.py
│   └── ...                         # 其他文件
│
├── ...其他aacode目录/                # aacode源代码--不变
│   ├── ...
│   └── ...
│ 
├── my_diffsynth_studio/            # 新增：是用户和Agent的工作目录
│   ├── .aacode/
│   ├── init.md
│   ├── outputs/
│   ├── programs/
│   ├── resources/            
│   └── ...
│ 
├── main.py                          # aacode源代码--不变
├── main_diffsynth.py                  # 项目主程序
├── README_aacode.md                 # aacode原有的README.md改为README_aacode.md
├── README.md                        # 新README.md
├── requrements.txt                  # 新的requirements.txt
└── ...                              # 其他文件不变


# 目录结构说明：
## aacode层面目录结构
* 保留aacode所有源目录结构（不过可去掉examples目录）
* aacode原来的README.md，改为README_aacode.md，英文版改为README_aacode_en.md，quick_start.md去掉。(原则上不管怎么改，aacode的编程能力都是存在的，原则上不修改aacode原本代码，可随着aacode的升级而升级)
* 可视情况由用户自己增加aacode的代码的skills。
* aacode根目录下增加README.md，作为Auto-DiffSynth-Studio项目的readme，以便于开源发布到github
* 增加my_diffsynth_studio目录，作为工作目录也即是用户唯一的工作目录，所有创作活动和结果，都在这个目录下。
* 增加main_diffsynth_tr.py，定死工作目录，添加适当的任务描述到当前任务，用户运行时运行的是这个程序。
## my_diffsynth_studio目录结构
* 结果放在outputs目录下
* 资源目录：resources,用于给用户存放一些资源，包括图片，数据等等
* 预置的程序文件：第一版事先开发的一些python程序，用于给agent使用，过程中Agent也会对程序进一步优化
## init.md包含信息
* 编程规范，原有的规则（核心规则、工作流程、代码质量）
* 资源目录（同时需要指明资源的存储路径）
## 预置的程序文件
* 待补充
* 待补充
## 其他
* 待补充



# 使用方式
## 常规使用
```bash
python3 main_diffsynth.py  "任务描述" 
# 原有的“-p”配置无效，项目目录固定在my_diffsynth_studio, 其他任务命令与aacode一致，只是主文件变为main_diffsynth.py
python main_diffsynth.py "任务描述" --plan-first
## 交互式连续对话
python main_diffsynth.py "任务描述" --interactive
## 指定会话
python main_diffsynth.py --session session_20250128_123456_0 "继续任务"
```






