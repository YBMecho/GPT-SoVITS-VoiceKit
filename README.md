# GPT-SoVITS VoiceKit 🎵

<p align="center">English | <a href="README.ZH.md">中文</a>  

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/platform-Windows-lightgrey)](https://www.microsoft.com/)

A powerful audio processing and training data generation toolkit specifically designed for the GPT-SoVITS voice synthesis model.

## ✨ Features

### 🎯 Voice Forge - Audio Processing Tool
- **🚀 GPU/CPU Hybrid Acceleration**: Supports NVIDIA GPU hardware acceleration with automatic detection and performance optimization
- **⚡ Parallel Processing**: Multi-process parallel processing significantly improves efficiency
- **🎵 Multi-format Support**: Supports WAV, MP3, FLAC, M4A, AAC, OGG, WMA and other audio formats
- **🔧 Adjustable Parameters**: Customizable sample rate, volume adjustment and other parameters
- **📁 Batch Processing**: Supports single file and directory batch processing
- **💻 Smart Detection**: Automatically detects GPU availability and provides detailed diagnostic information

### 📋 List Generator - Training List Generator  
- **🌍 Multilingual Support**: Supports 10 languages including Chinese, Japanese, English, Korean
- **📂 Recursive Search**: Automatically matches audio files with corresponding annotation texts
- **📝 Standard Format**: Generates GPT-SoVITS standard training format
- **🎯 Character Management**: Automatically extracts character names and organizes data
- **⚙️ Flexible Configuration**: Supports custom paths, formats and export locations

## 🛠️ Installation Instructions

### Requirements
- Python 3.8 or higher
- Windows 10/11 (Recommended)
- NVIDIA GPU (Optional, for GPU acceleration)

### Quick Installation

```bash
# Clone project
git clone https://github.com/YBMecho/GPT-SoVITS-VoiceKit.git
cd GPT-SoVITS-VoiceKit

# Install dependencies
pip install -r requirements.txt

# GPU version PyTorch (Optional, for GPU acceleration)
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

### Dependencies
```txt
torch>=2.0.0
numpy>=1.21.0
pathlib
argparse
multiprocessing
concurrent.futures
subprocess
```

## 🎵 Voice Forge Tutorial

### Basic Usage

```bash
# Process single audio file
python voice_forge.py input.wav

# Batch process folder
python voice_forge.py audio_folder/

# Specify output directory
python voice_forge.py audio_folder/ output_folder/

# Use GPU acceleration
python voice_forge.py audio_folder/ --device gpu

# Custom parameters
python voice_forge.py audio_folder/ --sample-rate 44100 --volume 1.2
```

### Parameter Description

| Parameter | Type | Default | Description |
|------|------|--------|------|
| `audio_path` | Required | - | Audio file or directory containing audio files |
| `output_path` | Optional | `processed_audio_with_frames` | Export audio path |
| `--device` | Optional | `hybrid` | Processing device: `hybrid`/`gpu`/`cpu` |
| `--sample-rate` | Optional | `32000` | Output audio sample rate |
| `--volume` | Optional | `1.0` | Volume adjustment multiplier |

### Processing Modes

- **Hybrid Mode** (Default): GPU+CPU hybrid parallel, automatic task allocation
- **GPU Mode**: Force GPU processing, requires CUDA support
- **CPU Mode**: Pure CPU parallel processing, best compatibility

### Example Scenarios

```bash
# Scenario 1: Fast batch processing (Recommended)
python voice_forge.py "original_audio/" --device hybrid

# Scenario 2: High-speed GPU processing
python voice_forge.py "original_audio/" "output/" --device gpu --sample-rate 48000

# Scenario 3: Low-configuration device processing
python voice_forge.py "original_audio/" --device cpu --volume 0.8

# Scenario 4: Custom output format
python voice_forge.py "original_audio/" "processed/" --sample-rate 22050 --volume 1.1
```

## 📋 List Generator Tutorial

### Basic Usage

```bash
# Generate training list
python list.py "acc/character1" "ZH" "original_audio/" "processed_audio_with_frames/" "wav"

# Specify export location
python list.py "acc/character1" "ZH" "original_audio/" "processed_audio_with_frames/" "wav" "output/"
```

### Parameter Description

| Position | Parameter | Type | Description | Example |
|------|------|------|------|------|
| 1 | `Path in list file` | Required | Fictional path prefix | `acc/character1` |
| 2 | `Language code` | Required | Audio content language | `ZH`, `JA`, `EN` |
| 3 | `Text path` | Required | Directory containing .lab files | `original_audio/` |
| 4 | `Audio folder path` | Optional | Audio file directory | `processed_audio_with_frames/` |
| 5 | `Audio format` | Optional | Audio file format | `wav` |
| 6 | `Export location` | Optional | Export file path | `output/` |

### Supported Language Codes

| Code | Language | Code | Language |
|------|------|------|------|
| `ZH` | Chinese | `JA` | Japanese |
| `EN` | English | `KO` | Korean |
| `ES` | Spanish | `FR` | French |
| `DE` | German | `IT` | Italian |
| `PT` | Portuguese | `RU` | Russian |

### File Structure Example

```
Project directory/
├── original_audio/          # Annotation text directory
│   ├── character1_001.lab
│   ├── character1_002.lab
│   └── ...
├── processed_audio_with_frames/  # Audio file directory
│   ├── character1_001.wav
│   ├── character1_002.wav
│   └── ...
└── opt.list              # Generated training list
```

### Output Format

```
acc/character1/character1_001.wav|character1|ZH|This is the content of the first sentence
acc/character1/character1_002.wav|character1|ZH|This is the content of the second sentence
```

## 💻 EXE Version Tutorial

### Download and Preparation

1. Download latest version from [Releases](../../releases) page
2. Extract to any directory
3. Ensure ffmpeg folder is in same directory as exe

### Voice Forge EXE Usage

```cmd
# Run in command line
voice_forge.exe "original_audio\" 

# View help
voice_forge.exe --help

# Use parameters
voice_forge.exe "original_audio\" "output\" --device hybrid --sample-rate 32000
```

### List Generator EXE Usage

```cmd
# Generate training list
list.exe "acc/character1" "ZH" "original_audio\" "processed_audio_with_frames\" "wav"

# View help and language support
list.exe
```

### Notes

- **Paths containing spaces**: Enclose path in double quotes
- **Chinese paths**: Ensure system supports UTF-8 encoding
- **Permission issues**: May require running as administrator
- **Antivirus software**: May need to be added to trusted list

## ⚡ Performance Optimization Tips

### GPU Acceleration Setup

1. **Check GPU support**
   ```bash
   python voice_forge.py --help  # View GPU detection info
   ```

2. **Install CUDA version PyTorch**
   ```bash
   pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
   ```

3. **Set environment variables** (Optional)
   ```bash
   set CUDA_VISIBLE_DEVICES=0
   ```

### Processing Speed Optimization

- **Small batch processing**: Process 500-1000 files at a time
- **SSD storage**: Use SSD for input/output files
- **Memory management**: Ensure sufficient system memory
- **Concurrency settings**: Hybrid mode automatically optimizes concurrency

## 🔧 Troubleshooting

### GPU Detection Issues

**Issue**: GPU not detected in virtual environment
```bash
# Solution: Install GPU version PyTorch
pip uninstall torch torchvision torchaudio
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

**Issue**: "PyTorch is CPU version" warning
```bash
# Check installed version
python -c "import torch; print(torch.__version__)"
# Should show version with cuda, e.g.: 2.7.1+cu118
```

### File Path Issues

**Issue**: EXE version can't find ffmpeg
- Ensure `ffmpeg-master-latest-win64-gpl-shared` folder is in same directory as exe
- Check folder contains `ffmpeg.exe` and `ffprobe.exe`

**Issue**: Chinese path garbled
- Ensure system locale supports UTF-8
- Using English path names can avoid encoding issues

### Processing Errors

**Issue**: WinError 2 system cannot find specified file
- Check input path is correct
- Ensure audio format is supported
- Verify ffmpeg components are complete

**Issue**: Insufficient memory error
- Reduce number of parallel processed files
- Use cpu mode instead of gpu mode
- Increase system virtual memory

## 🏗️ Development and Building

### Run from Source

```bash
git clone https://github.com/YBMecho/GPT-SoVITS-VoiceKit.git
cd GPT-SoVITS-VoiceKit
pip install -r requirements.txt
python voice_forge.py --help
```

### Package as EXE

```bash
# Install pyinstaller
pip install pyinstaller

# Package voice_forge
pyinstaller voice_forge.spec

# Package list generator
pyinstaller list.spec
```

### Custom Modifications

Program uses modular design, main components:

- **GPU detection module**: `detect_gpu()`, `detect_gpu_fallback()`
- **Audio processing module**: `process_audio_file()`, `get_audio_duration_frames()`
- **Parallel processing module**: `process_audio_worker()`
- **File search module**: `find_audio_files()`, `find_lab_file()`

## 🤝 Contribution Guide

Welcome code contributions and suggestions! Please follow these steps:

1. Fork this project
2. Create feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open Pull Request

### Reporting Issues

Please report issues on [Issues](../../issues) page, include:
- OS version
- Python version
- Screenshot of error message
- Reproduction steps

## 📄 License

This project is licensed under the [MIT License](LICENSE).

## 👨‍💻 Author Info

**YBMecho**
- QQ: 3350198579
- Email: 3350198579@qq.com
- GitHub: [@YBMecho](https://github.com/YBMecho)

## 🙏 Acknowledgements

- [GPT-SoVITS](https://github.com/RVC-Boss/GPT-SoVITS) - Excellent voice synthesis project
- [FFmpeg](https://ffmpeg.org/) - Powerful multimedia processing library
- [PyTorch](https://pytorch.org/) - Deep learning framework

---

If this project helps you, please give it a ⭐️!

[⬆️ Back to top](#gpt-sovits-voicekit-)
