# MCP Terminal Server - Windows Setup

## What is MCP?
MCP (Model Context Protocol) allows communication between external tools and AI-Client (here Claude-AI). This project sets up an MCP-compatible terminal server to execute shell commands within a defined workspace.

---

## Installing Claude for Desktop
1. Download and install **Claude for Desktop** from Claude's official website.
2. **Windows:** Follow the installer steps.
3. Open the application and log in.

---

## Step 1: Install `uv`
### Method 1: Standalone Installer
Run this command in **PowerShell**:
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

### Method 2: PyPI
If you have Python installed:
```powershell
pip install uv  # or
pipx install uv
```

**After installation, restart your terminal** so `uv` is recognized.

---

## Step 2: Create the MCP Directory Structure
Run the following commands in **PowerShell**:
```powershell
mkdir D:\path\to\mcp\servers\terminal_server
mkdir $env:USERPROFILE\mcp\workspace
```
- `D:\path\to\mcp\servers\terminal_server`: Stores all MCP servers.
- `$env:USERPROFILE\mcp\workspace`: Dedicated workspace directory.

---

## Step 3: Set Up a Python Project
```powershell
cd D:\path\to\mcp\servers\terminal_server
uv init
```
This initializes a Python project inside `terminal_server`.

---

## Step 4: Set Up a Virtual Environment
```powershell
uv venv
.venv\Scripts\activate
```
This creates and activates a virtual environment, keeping dependencies isolated.

---

## Step 5: Install Required Packages
```powershell
uv add "mcp[cli]"
```
This installs the MCP package to enable communication with Claude.

---

## Step 6: Run the MCP Terminal Server
```powershell
uv run terminal_server.py
```
This starts the terminal server within the virtual environment.

---

## Step 7: Configure Claude for Desktop
Edit the **Claude config file** at:
```
C:\Users\<your-username>\AppData\Roaming\Claude\claude_desktop_config.json
```

Add the following configuration:
```json
{
    "mcpServers": {
        "terminal": {
            "command": "C:\\path\\to\\uv.exe",
            "args": [
                "--directory", "D:\\path\\to\\mcp\\servers\\terminal_server",
                "run",
                "terminal_server.py"
            ]
        }
    }
}
```

### **Final Step: Restart Claude for Desktop**
Once restarted, you should see a **hammer icon**, meaning your tool is ready to use! 🚀
