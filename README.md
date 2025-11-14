# Real-time STT - 实时语音转文字工具

这是一个基于 PySide6 和 [Sherpa-Onnx](https://github.com/k2-fsa/sherpa-onnx) 开发的桌面应用，能够将你的中文（及中英混合）语音实时转换为带标点符号的文字。它非常适合用于会议记录、课堂笔记、语音写作等场景。

---

## 界面截图

**主界面:**
![realtimestt0 1](https://github.com/user-attachments/assets/503e33c2-188b-424a-b3d8-b2949674e7ac)



## 主要功能

*   **🎤 实时识别**: 延迟低于2秒，实现语音到文字的实时转换。
*   **✍️ 自动标点**: 转录完成后，自动为生成的文本段落添加合适的标点符号。
*   **📋 结果处理**:
    *   **导出为 TXT**: 一键将所有转录内容保存为 `.txt` 文件。
    *   **一键复制**: 方便地将结果复制到剪贴板。
    *   **清空内容**: 快速清除已有的转录文本。
*   **💾 录音保存**: 在进行实时转录的同时，自动将麦克风输入保存为 `.wav` 格式的音频文件，方便后续回听和校对。
*   **⚙️ 设备选择**: 自动检测并允许用户选择不同的麦克风设备。
*   **跨平台**: 基于 Python 和 PySide6，理论上支持 Windows, macOS 和 Linux。

## 安装与运行

我们推荐使用 [uv](https://github.com/astral-sh/uv) 进行环境管理和依赖安装，因为它使用简单、速度极快。

### 步骤 1: 环境准备

1.  **安装 uv**:
    *   **macOS / Linux**:
        ```bash
        curl -LsSf https://astral.sh/uv/install.sh | sh
        ```
    *   **Windows**: 开始菜单-找到 Windows PowerShell 打开
        ```powershell
        powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
        ```

2.  **安装 FFmpeg** :
    *   **macOS**: `brew install ffmpeg`
    *   **Ubuntu/Debian**: `sudo apt update && sudo apt install ffmpeg`
    *   **Windows**: 下载解压，将exe文件放在本项目目录下即可  https://www.gyan.dev/ffmpeg/builds/ffmpeg-release-full.7z 

### 步骤 2: 克隆项目并下载模型 

1.  **克隆本仓库**:
    ```bash
    git clone https://github.com/jianchang512/realtime-stt.git
    cd realtime-stt
    ```

2.  **创建 `onnx` 文件夹并下载模型**:
    应用运行需要依赖 Sherpa-Onnx 模型文件。
    ```bash
    mkdir onnx
    ```
    *   **下载模型**: [点击这里下载模型 (realtimestt-models.7z)](https://github.com/jianchang512/realtime-stt/releases/download/v0.0/realtimestt-models.7z)
    *   **放置模型**: 下载完成后，解压 `realtimestt-models.7z` 文件，将其中的 **4个模型文件** (`ctc.model.onnx`, `decoder.onnx`, `encoder.onnx`, `tokens.txt`) 移动到刚刚创建的 `onnx` 文件夹内。

    完成后的目录结构应如下所示：
    ```
    realtime-stt/
    ├── onnx/
    │   ├── ctc.model.onnx
    │   ├── decoder.onnx
    │   ├── encoder.onnx
    │   └── tokens.txt
    └── stt.py
    ```

### 步骤 3: 运行应用

在项目根目录下，打开终端并执行以下命令：

```bash
uv sync
```

`uv` 会自动创建一个虚拟环境，安装所有必要的依赖包 (`PySide6`, `sherpa-onnx`, `sounddevice` 等)，然后启动应用程序。

### 使用方法

1.  启动应用后，从下拉菜单中选择正确的麦克风设备。
2.  点击 **"启动实时语音转文字"** 按钮。
3.  开始说话，识别的中间结果会显示在上方文本框中。
4.  当您停顿一段时间后，一句完整的话会自动整理并添加标点，显示在下方的主文本区域。
5.  点击 **"正在语音转文字中..."** 按钮可以停止转录。
6.  所有录音文件（`.wav`）和对应的文本记录（`.txt`）会自动保存在 `output` 文件夹中。

## 预构建包

如果你不想手动配置环境，可以直接下载为 Windows 用户准备的预构建包。

➡️ [**前往 Releases 页面下载**](https://github.com/jianchang512/realtime-stt/releases)

下载后解压即可运行，无需安装 Python 或其他依赖。

## 致谢

*   **核心实时引擎**: [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx)
*   **GUI 框架**: [PySide6](https://www.qt.io/qt-for-python)
*   **语音识别引擎**: [sherpa-onnx](https://github.com/k2-fsa/sherpa-onnx)
*   **ONNX 推理**: [onnxruntime](https://onnxruntime.ai/)
*   **音频 I/O**: [sounddevice](https://python-sounddevice.readthedocs.io/)
*   **数值计算**: [NumPy](https://numpy.org/)


