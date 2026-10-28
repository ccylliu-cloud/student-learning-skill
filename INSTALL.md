# 安装与首次使用

## 让Agent协助安装

推荐把仓库README中的安装提示复制给你的Codex或WorkBuddy。也可以下载Release中的完整ZIP、解压后，把整个文件夹交给Agent，让它读取本指南。

## 安装前

- 使用可以读写本机文件、运行Python的桌面Agent。只有网页聊天界面或只有阅读权限时，无法完成本地安装。
- 准备Python 3.10+，主要验收版本3.12。解压后的文件夹应同时有install.py、LICENSE和student-learning，不要只复制SKILL.md。
- 已有同名Skill或学生资料时先保留原件并备份，选择新的安装目录；安装器拒绝覆盖旧目录。
- 个人/家庭非商业用途按LICENSE免费使用；宿主或模型费用由宿主提供。

## Codex

在解压文件夹运行（如系统命令为python3，请相应替换python）：

```bash
python install.py --host codex
```

默认安装到用户目录下的`.codex/skills/student-learning`。已存在时停止并由Agent检查，不要直接删除。安装器输出实际target和下一步命令。

## WorkBuddy

先在WorkBuddy中打开一个用于学习档案的本地项目。请Agent把以下占位路径替换为该项目真实绝对路径后执行：

```bash
python install.py --host workbuddy --workspace "项目绝对目录" --target "项目绝对目录/.workbuddy/skills/student-learning"
```

所有路径使用当前项目内部位置。Skill代码放`.workbuddy/skills/student-learning`，学生档案放项目内独立的“学习档案”目录，不把数据库放入Skill代码目录。如果当前WorkBuddy版本使用其他Skill发现位置，请让Agent按该宿主实际规则配置并保持target位于当前项目；不要误选Codex宿主标记。

## 两宿主安装后的步骤

1. 按安装器输出，在新安装中运行`python scripts/setup_runtime.py --install-deps`。WorkBuddy加`--workspace "项目绝对目录"`。这一步联网获取缺少的Python依赖，只写本安装runtime/venv，不替换系统Python。
2. 后续使用setup输出的独立Python解释器。运行`scripts/portable.py doctor`检查版本、资源、依赖和知识库。首次姓名、年级和档案位置由家长填写确认。
3. 使用同一个独立解释器运行`scripts/portable.py init`初始化三科知识记录，再运行`scripts/portable.py serve --port 8767 --open`启动页面。每条命令都要基于真实安装目录，不在解压目录混用路径。预期知识记录数学1211、英语355、语文84；不是演示学生题目。
4. 打开返回的127.0.0.1本地地址。端口被占用时换空闲端口，不结束其他项目的服务。关闭本服务的终端或Ctrl+C可以停止，源文件和学生档案仍保留。
5. 完成后请Agent列出实际Skill目录、档案目录、本地地址以及下一次启动命令。Skill未被宿主发现时，新开一轮对话并明确让Agent读取安装目录的SKILL.md。

完整协议位于解压后的`student-learning/references/trial-installation.md`。Mac也可使用安装目录中的“启动学习档案.command”；Windows请让Agent按setup输出的Python路径启动。

## 第一次试用

推荐先试合成材料：让Agent读取TESTING.md并生成合成试卷。上传分组后只识别批改错题，结果待家长复核，不要自动确认错因或掌握。

WorkBuddy页面显示“等待对话处理”时，在同一项目对话发送：

> 使用已安装的student-learning Skill，处理网页保存的待识别试卷；保留已有请求和圈选，完成后告诉我回页面复核。不要重复新建同一张卷或重读已经完成的阶段。

Codex后台模型不可用时，请Agent检查本安装识别配置，明确告诉你可用性；不暗中更换模型。不能看图时应停止并保留任务，不能生成猜测结果。

## 更新与资料保护

新版本安装到新目录，旧档案先在线备份。复用旧档案须明确指定并核对，不能静默新建第二份或复制运行中的数据库。不要把学生图片、数据库或运行日志推送到本仓库。HEIC依赖环境未全部验收，遇到问题优先使用清晰原始JPG/PNG；不要用截图假装原片。
