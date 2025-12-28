# 🛠️ MOIS_1_FONDATIONS/PREREQUISITES_INSTALLATION.md : Prerequisites and Installation

## 🎯 Objectives

This guide helps you configure your development environment to follow the Accelerated Python program. We cover prerequisites, recommended IDEs, Python installation on Windows and Ubuntu, as well as the creation and activation of virtual environments.

-----

## 1. 📋 Prerequisites

Before starting, make sure you have:
- A computer with **Windows 10/11** or **Ubuntu 20.04/22.04** (or an equivalent Linux distribution).
- A stable internet connection for downloading software.
- Administrative rights to install software (if necessary).

-----

## 2. 💻 Recommended IDEs

An Integrated Development Environment (IDE) makes writing and debugging code easier. Here are popular options:
- **Visual Studio Code (VSCode)**: Recommended for this program (lightweight, customizable, native Python support).
- **PyCharm**: Ideal for complex projects (free Community version available).
- **Jupyter Notebook**: Perfect for data exploration (used in Month 6).
- **Thonny**: Simple, suitable for beginners.

We will use **VSCode** as the primary IDE in this guide.

-----

## 3. 🐍 Python Installation

### On Windows
1. Download the latest version of Python (recommended: 3.11 or higher) from [python.org](https://www.python.org/downloads/).
2. Run the installer and check **"Add Python to PATH"**.
3. Follow the instructions, choose "Install Now", and leave the settings as default.
4. Verify the installation by opening a command prompt (`cmd`) and typing:
   ```bash
   python --version
   ```
   You should see something like `Python 3.11.5`.

### On Ubuntu
1. Update packages:
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```
2. Install Python and development tools:
   ```bash
   sudo apt install python3 python3-pip python3-venv -y
   ```
3. Verify the installation in a terminal:
   ```bash
   python3 --version
   ```
   Expected result: `Python 3.11.x`.

-----

## 4. 🌐 Creating and Activating a Virtual Environment

Virtual environments isolate dependencies per project, an essential practice for reproducibility.

### On Windows
1. Create a folder for your project (e.g., `MOIS_1_FONDATIONS`):
   ```bash
   mkdir MOIS_1_FONDATIONS
   cd MOIS_1_FONDATIONS
   ```
2. Create a virtual environment:
   ```bash
   python -m venv .venv
   ```
3. Activate it:
   ```bash
   .venv\Scripts\activate
   ```
   You will see `(.venv)` appearing before your command prompt.

### On Ubuntu
1. Create a folder for your project:
   ```bash
   mkdir MOIS_1_FONDATIONS
   cd MOIS_1_FONDATIONS
   ```
2. Create a virtual environment:
   ```bash
   python3 -m venv .venv
   ```
3. Activate it:
   ```bash
   source .venv/bin/activate
   ```
   You will see `(.venv)` before your command prompt.

-----

## 5. ⚙️ VSCode Configuration
1. Download and install VSCode from [code.visualstudio.com](https://code.visualstudio.com/).
2. Install the **Python** extension (by Microsoft) via the Extensions tab.
3. Open the `MOIS_1_FONDATIONS` folder in VSCode.
4. Select the virtual environment's Python interpreter:
   - Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac).
   - Type "Python: Select Interpreter" and choose `./.venv/bin/python` (Ubuntu) or `./.venv/Scripts/python.exe` (Windows).
5. Create a `.vscode/settings.json` file with:
   ```json
   {
       "python.linting.enabled": true,
       "python.linting.pylintEnabled": true,
       "python.formatting.provider": "black"
   }
   ```
   This enables PEP 8 checking and auto-formatting.

-----

## 6. 📦 Installing Dependencies
1. Create a `requirements.txt` file in `MOIS_1_FONDATIONS` with:
   ```
   pytest
   ```
2. Install the dependencies in the virtual environment:
   - On Windows: `pip install -r requirements.txt`
   - On Ubuntu: `pip3 install -r requirements.txt`
3. Verify the installation with:
   ```bash
   pip list
   ```
   You should see `pytest` in the list.

-----

## ⏳ Conclusion
You are now ready to code! Test your setup by creating a `test.py` file with:
```python
print("Environment ready!")
```
Run it with `python test.py` (Windows) or `python3 test.py` (Ubuntu). To deactivate the virtual environment, use `deactivate` on both systems.

**Preparation W1:** Consult `WEEK_1_Syntaxe_Types.md` to start with Python syntax.
