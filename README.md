# ToolBox

A PySide6 Windows desktop toolbox that bundles everyday utilities into one visual interface.

PySide6 写的 Windows 桌面工具箱，把一堆常用小工具收进同一个带导航栏的 GUI 里。

---

## Overview / 概述

ToolBox is for people who write a lot of throwaway scripts and want them organized. It provides a sidebar-navigated GUI that auto-discovers modules at startup — any `QWidget` subclass dropped into `Modules/` becomes a switchable page. Adding a new tool is as simple as dropping a file into the directory.

给平时写很多零碎脚本的人用的。主程序启动时自动扫描 `Modules/` 目录，凡是继承 `QWidget` 的类都会被加载为一个可切换页面。加工具就是往目录里丢文件，就这么简单。

## Features / 功能

### Main GUI Modules (主界面模块)

| Module | Description |
|--------|-------------|
| **FileClassifierTool** | Filter/exclude folders by type, generate file relationship trees, right-click to open |
| **TranslationTool** | Tencent Cloud TMT-based translation with hotkey/clipboard support, multi-target language |
| **YuShengJun** | Web scraper — fetches page content by URL, powered by BeautifulSoup, newspaper, yt-dlp |
| **Setting** | UI style switching, background image, text color, interface language |

| 模块 | 说明 |
|------|------|
| **FileClassifierTool** | 按类型过滤/排除文件夹，生成文件关系树，右键打开 |
| **TranslationTool** | 基于腾讯云 TMT 的划词/快捷键翻译，支持多目标语言与热键 |
| **YuShengJun** | 网页爬虫，根据 URL 抓内容，依赖 BeautifulSoup、newspaper、yt-dlp |
| **Setting** | 切换 UI 风格、背景图片、文本颜色、界面语言 |

### Standalone Scripts (`programtool/`) / 独立脚本工具

- **CodeCleaner.py** — Code cleanup utility / 代码清理
- **ConverterGUI.py** — PyQt6 to PySide6 code converter / PyQt6 转 PySide6 转换器
- **FileClassifierTool.py** — Standalone file classifier (reads/writes `config.cfg`) / 独立版文件分类工具
- **LibUninstaller.py** — Batch uninstall Python packages / 批量卸载 Python 库
- **QRCGenerator.py** — Qt `.qrc` resource file generator / Qt 资源文件生成器

### Experimental Modules (`noplease/`) / 实验模块

`top/dwgx/Modules/noplease/` contains experimental and historical code: `SystemCore`, `SystemTool`, `WiFiHacker`, etc. These are not loaded by default (the module manager only scans the top-level `Modules/` directory).

`noplease/` 下是实验性/历史代码（`SystemCore`、`SystemTool`、`WiFiHacker` 等），默认不会被主程序加载。

## Tech Stack / 技术栈

- **Language:** Python 3.10+
- **GUI:** PySide6
- **Dependencies:**
  - `PySide6`, `beautifulsoup4`, `newspaper3k`, `yt-dlp`
  - `tencentcloud-sdk-python`, `keyboard`, `pyperclip`
  - `pywifi`, `comtypes`

## Project Structure / 项目结构

```
ToolBox/
├── top/
│   ├── dwgx/
│   │   ├── Client.py            # Entry point / 主程序入口
│   │   ├── Manager/             # Config & module management
│   │   │   ├── ConfigManager.py
│   │   │   └── ModuleManager.py
│   │   ├── Modules/             # GUI modules (auto-loaded)
│   │   │   ├── FileClassifierTool.py
│   │   │   ├── TranslationTool.py
│   │   │   ├── YuShengJun.py
│   │   │   ├── Setting.py
│   │   │   └── noplease/        # Experimental / historical
│   │   └── utils/               # Icons, logging, translation core
│   └── resource/                # Icons, backgrounds, Qt resources
├── programtool/                 # Standalone script tools
├── requirements                 # Dependencies
└── LICENSE                      # GNU GPL v3.0
```

## Getting Started / 快速开始

**Prerequisites / 前置要求:**

- Python 3.10+ <!-- TODO: 确认最低支持版本 -->
- Windows

**Install & Run / 安装运行:**

```bash
git clone https://github.com/dwgx/ToolBox.git
cd ToolBox
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements
python top/dwgx/Client.py
```

<!-- TODO: 确认主程序的推荐运行工作目录（模块与资源路径解析依赖启动位置）。 -->

Standalone scripts can be run directly / 独立脚本可以直接运行：

```bash
python programtool/LibUninstaller.py
```

## Configuration / 配置

The main app reads/writes `config.json` via `ConfigManager` (auto-generated on first run), containing sections: `translation`, `file_classifier`, `ui_settings`.

主程序通过 `ConfigManager` 读写 `config.json`（首次运行自动生成），包含 `translation`、`file_classifier`、`ui_settings` 三个分区。

`programtool/FileClassifierTool.py` uses a separate `config.cfg` (INI format) for scan directories and filter rules.

**Translation API credentials / 翻译 API 凭据:**

The translation module requires Tencent Cloud TMT credentials (`SECRET_ID`, `SECRET_KEY`), configurable via the Settings dialog.

翻译模块需要腾讯云 TMT 凭据（`SECRET_ID`、`SECRET_KEY`），在设置对话框里填。

## Status / 状态

Personal project, WIP. Some modules (especially under `noplease/`) are experimental or historical code.

个人项目，WIP 状态。`noplease/` 下的东西属于实验/历史代码，留着当成长记录。

## License / 许可证

[GNU General Public License v3.0](LICENSE)
