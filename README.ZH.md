# GPT-SoVITS VoiceKit 🎵

<p align="center"><a href="README.md">English</a> | 中文  


[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/platform-Windows-lightgrey)](https://www.microsoft.com/)

一个强大的音频处理和训练数据生成工具套件，专为GPT-SoVITS语音合成模型设计。

## ✨ 功能特性

### 🎯 Voice Forge - 音频处理工具
- **🚀 GPU/CPU混合加速**: 支持NVIDIA GPU硬件加速，自动检测并优化处理性能
- **⚡ 并行处理**: 多进程并行处理，大幅提升处理效率
- **🎵 多格式支持**: 支持WAV、MP3、FLAC、M4A、AAC、OGG、WMA等音频格式
- **🔧 参数可调**: 自定义采样率、音量调整等参数
- **📁 批量处理**: 支持单文件和目录批量处理
- **💻 智能检测**: 自动检测GPU可用性，提供详细诊断信息

### 📋 List Generator - 训练清单生成器  
- **🌍 多语言支持**: 支持中文、日语、英语、韩语等10种语言
- **📂 递归搜索**: 自动匹配音频文件和对应的标注文本
- **📝 格式标准**: 生成GPT-SoVITS标准训练格式
- **🎯 角色管理**: 自动提取角色名称并组织数据
- **⚙️ 灵活配置**: 支持自定义路径、格式和导出位置

## 🛠️ 安装说明

### 环境要求
- Python 3.8 或更高版本
- Windows 10/11 (推荐)
- NVIDIA GPU (可选，用于GPU加速)

### 快速安装

```bash
# 克隆项目
git clone https://github.com/YBMecho/GPT-SoVITS-VoiceKit.git
cd GPT-SoVITS-VoiceKit

# 安装依赖
pip install -r requirements.txt

# GPU版本PyTorch (可选，用于GPU加速)
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

### 依赖库
```txt
torch>=2.0.0
numpy>=1.21.0
pathlib
argparse
multiprocessing
concurrent.futures
subprocess
```

## 🎵 Voice Forge 使用教程

### 基本用法

```bash
# 处理单个音频文件
python voice_forge.py input.wav

# 批量处理文件夹
python voice_forge.py audio_folder/

# 指定输出目录
python voice_forge.py audio_folder/ output_folder/

# 使用GPU加速
python voice_forge.py audio_folder/ --device gpu

# 自定义参数
python voice_forge.py audio_folder/ --sample-rate 44100 --volume 1.2
```

### 参数说明

| 参数 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `audio_path` | 必需 | - | 音频文件或包含音频文件的目录 |
| `output_path` | 可选 | `processed_audio_with_frames` | 导出音频路径 |
| `--device` | 可选 | `hybrid` | 处理设备: `hybrid`/`gpu`/`cpu` |
| `--sample-rate` | 可选 | `32000` | 输出音频采样率 |
| `--volume` | 可选 | `1.0` | 音量调整倍数 |

### 处理模式说明

- **hybrid模式** (默认): GPU+CPU混合并行，自动分配任务
- **gpu模式**: 强制使用GPU处理，需要CUDA支持
- **cpu模式**: 纯CPU并行处理，兼容性最好

### 示例场景

```bash
# 场景1: 快速批量处理 (推荐)
python voice_forge.py "原始声音/" --device hybrid

# 场景2: GPU高速处理
python voice_forge.py "原始声音/" "output/" --device gpu --sample-rate 48000

# 场景3: 低配置设备处理
python voice_forge.py "原始声音/" --device cpu --volume 0.8

# 场景4: 自定义输出格式
python voice_forge.py "原始声音/" "processed/" --sample-rate 22050 --volume 1.1
```

## 📋 List Generator 使用教程

### 基本用法

```bash
# 生成训练清单
python list.py "acc/character1" "ZH" "原始声音/" "processed_audio_with_frames/" "wav"

# 指定导出位置
python list.py "acc/character1" "ZH" "原始声音/" "processed_audio_with_frames/" "wav" "output/"
```

### 参数说明

| 位置 | 参数 | 类型 | 说明 | 示例 |
|------|------|------|------|------|
| 1 | `list文件里的路径` | 必需 | 虚构的路径前缀 | `acc/character1` |
| 2 | `语言代码` | 必需 | 音频内容的语言 | `ZH`, `JA`, `EN` |
| 3 | `音频文字路径` | 必需 | 存放.lab文件的目录 | `原始声音/` |
| 4 | `音频文件夹路径` | 可选 | 音频文件目录 | `processed_audio_with_frames/` |
| 5 | `音频格式` | 可选 | 音频文件格式 | `wav` |
| 6 | `导出位置` | 可选 | 导出文件路径 | `output/` |

### 支持的语言代码

| 代码 | 语言 | 代码 | 语言 |
|------|------|------|------|
| `ZH` | 中文 | `JA` | 日本語 |
| `EN` | English | `KO` | 한국어 |
| `ES` | Español | `FR` | Français |
| `DE` | Deutsch | `IT` | Italiano |
| `PT` | Português | `RU` | Русский |

### 文件结构示例

```
项目目录/
├── 原始声音/              # 标注文本目录
│   ├── character1_001.lab
│   ├── character1_002.lab
│   └── ...
├── processed_audio_with_frames/  # 音频文件目录
│   ├── character1_001.wav
│   ├── character1_002.wav
│   └── ...
└── opt.list              # 生成的训练清单
```

### 输出格式

```
acc/character1/character1_001.wav|character1|ZH|这是第一句话的内容
acc/character1/character1_002.wav|character1|ZH|这是第二句话的内容
```

## 💻 EXE版本使用教程

### 下载和准备

1. 从 [Releases](../../releases) 页面下载最新版本
2. 解压到任意目录
3. 确保ffmpeg文件夹在exe同目录下

### Voice Forge EXE 使用

```cmd
# 在命令行中运行
voice_forge.exe "原始声音\" 

# 查看帮助
voice_forge.exe --help

# 使用参数
voice_forge.exe "原始声音\" "output\" --device hybrid --sample-rate 32000
```

### List Generator EXE 使用

```cmd
# 生成训练清单
list.exe "acc/character1" "ZH" "原始声音\" "processed_audio_with_frames\" "wav"

# 查看帮助和语言支持
list.exe
```

### 注意事项

- **路径中包含空格**: 请使用双引号包围路径
- **中文路径**: 确保系统支持UTF-8编码
- **权限问题**: 以管理员身份运行可能需要
- **杀毒软件**: 可能需要添加到信任列表

## ⚡ 性能优化建议

### GPU加速设置

1. **检查GPU支持**
   ```bash
   python voice_forge.py --help  # 查看GPU检测信息
   ```

2. **安装CUDA版PyTorch**
   ```bash
   pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
   ```

3. **设置环境变量** (可选)
   ```bash
   set CUDA_VISIBLE_DEVICES=0
   ```

### 处理速度优化

- **小批量处理**: 每次处理500-1000个文件
- **SSD存储**: 使用SSD存储输入输出文件
- **内存管理**: 确保有足够的系统内存
- **并发设置**: hybrid模式会自动优化并发数

## 🔧 常见问题解决

### GPU检测问题

**问题**: 虚拟环境中检测不到GPU
```bash
# 解决方案: 安装GPU版PyTorch
pip uninstall torch torchvision torchaudio
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

**问题**: 提示"PyTorch为CPU版本"
```bash
# 检查安装的版本
python -c "import torch; print(torch.__version__)"
# 应该显示包含cuda的版本号，如: 2.7.1+cu118
```

### 文件路径问题

**问题**: exe版本找不到ffmpeg
- 确保`ffmpeg-master-latest-win64-gpl-shared`文件夹与exe在同一目录
- 检查文件夹内是否包含`ffmpeg.exe`和`ffprobe.exe`

**问题**: 中文路径乱码
- 确保系统区域设置支持UTF-8
- 使用英文路径名可以避免编码问题

### 处理错误

**问题**: WinError 2 系统找不到指定的文件
- 检查输入路径是否正确
- 确保音频文件格式受支持
- 验证ffmpeg组件是否完整

**问题**: 内存不足错误
- 减少并行处理的文件数量
- 使用cpu模式而非gpu模式
- 增加系统虚拟内存

## 🏗️ 开发和构建

### 从源码运行

```bash
git clone https://github.com/YBMecho/GPT-SoVITS-VoiceKit.git
cd GPT-SoVITS-VoiceKit
pip install -r requirements.txt
python voice_forge.py --help
```

### 打包为EXE

```bash
# 安装pyinstaller
pip install pyinstaller

# 打包voice_forge
pyinstaller voice_forge.spec

# 打包list generator
pyinstaller list.spec
```

### 自定义修改

程序采用模块化设计，主要组件：

- **GPU检测模块**: `detect_gpu()`, `detect_gpu_fallback()`
- **音频处理模块**: `process_audio_file()`, `get_audio_duration_frames()`
- **并行处理模块**: `process_audio_worker()`
- **文件搜索模块**: `find_audio_files()`, `find_lab_file()`

## 🤝 贡献指南

欢迎贡献代码和建议！请遵循以下步骤：

1. Fork 本项目
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 开启 Pull Request

### 报告问题

请在 [Issues](../../issues) 页面报告问题，包含以下信息：
- 操作系统版本
- Python版本
- 错误信息截图
- 复现步骤

## 📄 许可证

本项目基于 [MIT License](LICENSE) 开源协议。

## 👨‍💻 作者信息

**YBMecho**
- QQ: 3350198579
- 邮箱: 3350198579@qq.com
- GitHub: [@YBMecho](https://github.com/YBMecho)

## 🙏 致谢

- [GPT-SoVITS](https://github.com/RVC-Boss/GPT-SoVITS) - 优秀的语音合成项目
- [FFmpeg](https://ffmpeg.org/) - 强大的多媒体处理库
- [PyTorch](https://pytorch.org/) - 深度学习框架

---

如果这个项目对您有帮助，请给个⭐️支持一下！

[⬆️ 回到顶部](#gpt-sovits-voicekit-)
