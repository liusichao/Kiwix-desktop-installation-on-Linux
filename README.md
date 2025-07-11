# win10如何安装Chocolatey、scoop

## 在 Windows 10 上安装 **Chocolatey** 和 **Scoop** 这两个包管理器可以极大简化软件安装和管理流程。以下是详细的安装步骤及注意事项：

---

## **一、安装 Chocolatey（Windows 包管理器）**
Chocolatey 是 Windows 上最流行的包管理器，支持通过命令行安装、升级和卸载软件。

### **1. 安装前提**
- **管理员权限**：需以管理员身份运行 PowerShell。
- **关闭杀毒软件**：部分杀毒软件可能拦截安装脚本（如 360、火绒等），建议临时关闭。
- **启用 PowerShell 脚本执行**：默认禁止运行脚本，需手动启用。

### **2. 安装步骤**
1. **以管理员身份打开 PowerShell**：
   - 按 `Win + X`，选择 **Windows PowerShell（管理员）** 或 **终端（管理员）**。

2. **设置脚本执行策略**：
   ```powershell
   Set-ExecutionPolicy Bypass -Scope Process -Force
   ```
   - 此命令仅对当前会话生效，避免全局修改策略。

3. **运行 Chocolatey 安装脚本**：
   ```powershell
   iwr https://community.chocolatey.org/install.ps1 -UseBasicParsing | iex
   ```
   - 或使用备用地址（若官方脚本被拦截）：
     ```powershell
     iwr https://chocolatey.org/install.ps1 -UseBasicParsing | iex
     ```

4. **验证安装**：
   ```powershell
   choco -v
   ```
   - 输出版本号（如 `1.6.0`）即表示安装成功。

### **3. 使用示例**
- **安装软件**：
  ```powershell
  choco install git -y  # 安装 Git
  choco install vscode -y  # 安装 VS Code
  ```
- **升级所有软件**：
  ```powershell
  choco upgrade all -y
  ```
- **卸载软件**：
  ```powershell
  choco uninstall git -y
  ```

### **4. 常见问题**
- **安装失败**：检查网络是否正常，或尝试关闭代理/VPN。
- **权限错误**：确保以管理员身份运行 PowerShell。
- **脚本被拦截**：临时关闭杀毒软件，或手动下载脚本并执行。

---

## **二、安装 Scoop（轻量级包管理器）**
Scoop 是另一个流行的 Windows 包管理器，专注于命令行工具和便携软件，无需管理员权限即可安装到用户目录。

### **1. 安装前提**
- **PowerShell 5+**：Windows 10 默认已满足。
- **启用 PowerShell 脚本执行**：需允许远程脚本运行。
- **推荐安装到默认目录**：`C:\Users\<用户名>\scoop`（避免空格和中文路径）。

### **2. 安装步骤**
1. **以普通用户身份打开 PowerShell**（无需管理员权限）：
   - 按 `Win + R`，输入 `powershell`，回车。

2. **设置脚本执行策略**：
   ```powershell
   Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
   ```
   - 仅对当前用户生效，允许运行本地脚本和远程签名脚本。

3. **安装 Scoop**：
   ```powershell
   iwr -useb get.scoop.sh | iex
   ```
   - 若安装失败，可能是网络问题，可尝试：
     ```powershell
     [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
     iwr -useb https://raw.githubusercontent.com/ScoopInstaller/Install/master/install.ps1 | iex
     ```

4. **验证安装**：
   ```powershell
   scoop --version
   ```
   - 输出版本号（如 `0.1.0`）即表示安装成功。

### **3. 配置 Scoop（可选）**
- **添加额外仓库**（如 `extras` 仓库，包含更多软件）：
  ```powershell
  scoop bucket add extras
  ```
- **更改安装目录**（如安装到 `D:\scoop`）：
  ```powershell
  $env:SCOOP='D:\scoop'
  [environment]::setEnvironmentVariable('SCOOP', $env:SCOOP, 'User')
  scoop install git  # 重新初始化 Scoop
  ```

### **4. 使用示例**
- **安装软件**：
  ```powershell
  scoop install git  # 安装 Git
  scoop install 7zip  # 安装 7-Zip
  scoop install sudo  # 安装 sudo（提升权限工具）
  ```
- **升级所有软件**：
  ```powershell
  scoop update *
  ```
- **卸载软件**：
  ```powershell
  scoop uninstall git
  ```

### **5. 常见问题**
- **安装失败**：检查网络是否正常，或尝试更换 DNS（如 `8.8.8.8`）。
- **权限错误**：确保脚本执行策略为 `RemoteSigned` 或 `Bypass`。
- **软件找不到**：安装 `extras` 仓库后重试：
  ```powershell
  scoop bucket add extras
  scoop install vscode  # 通过 extras 仓库安装
  ```

---

## **三、Chocolatey vs Scoop：如何选择？**
| **特性**         | **Chocolatey**                     | **Scoop**                          |
|------------------|-----------------------------------|------------------------------------|
| **安装权限**     | 需要管理员权限                    | 无需管理员权限（默认安装到用户目录） |
| **软件范围**     | 包含 GUI 软件和系统工具            | 专注于命令行工具和便携软件          |
| **安装方式**     | 支持系统级安装（如 `C:\Program Files`） | 默认安装到用户目录（如 `~/scoop/apps`） |
| **速度**         | 较慢（需下载安装包）              | 较快（直接解压便携版）             |
| **适合场景**     | 管理系统级软件（如 Chrome、Office） | 管理开发工具（如 Git、Node.js）    |

### **推荐组合使用**
- **系统软件**：用 Chocolatey 安装（如 Chrome、VS Code）。
- **开发工具**：用 Scoop 安装（如 Git、Node.js、Ripgrep）。

---

## **四、总结**
1. **Chocolatey**：
   - 管理员权限运行 PowerShell。
   - 执行安装脚本：`iwr https://community.chocolatey.org/install.ps1 -UseBasicParsing | iex`。
   - 验证：`choco -v`。

2. **Scoop**：
   - 普通用户运行 PowerShell。
   - 设置执行策略：`Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force`。
   - 执行安装脚本：`iwr -useb get.scoop.sh | iex`。
   - 验证：`scoop --version`。

按需选择或组合使用这两个工具，可以大幅提升 Windows 10 的软件管理效率！

---

# win10除Chocolatey 和 Scoop之外还有哪些可以安装的?

## 在 Windows 10 上，除了 **Chocolatey** 和 **Scoop**，还有以下包管理器可供选择，它们各有特色，适用于不同场景：

### **1. Winget（微软官方包管理器）**
- **特点**：
  - **官方支持**：由微软推出，集成在 Windows 10 1709 及以上版本中，可通过 Microsoft Store 自动更新。
  - **安装便捷**：直接通过 PowerShell 命令或 Microsoft Store 安装。
  - **软件源丰富**：支持从 Microsoft Store、GitHub 等源安装软件，覆盖主流应用。
  - **命令简洁**：与 Linux 的 `apt` 类似，适合快速安装、更新和卸载软件。
- **适用场景**：
  - 适合普通用户，尤其是偏好官方工具、追求稳定性的用户。
  - 与 Windows 系统深度集成，适合管理系统级软件（如 Chrome、VS Code）。
- **安装命令**：
  ```powershell
  # 通过 Microsoft Store 安装（推荐）
  # 或手动安装（需开启开发者模式）
  irm https://aka.ms/winget-latest.appxbundle -OutFile winget.appxbundle
  Add-AppxPackage .\winget.appxbundle
  ```
- **使用示例**：
  ```powershell
  winget search vscode  # 搜索软件
  winget install Microsoft.VisualStudioCode  # 安装 VS Code
  winget upgrade  # 更新所有软件
  ```

### **2. Npackd（开源包管理器）**
- **特点**：
  - **开源免费**：支持图形界面和命令行操作。
  - **多软件源**：支持自定义软件源，可添加第三方仓库。
  - **依赖管理**：自动解决软件依赖关系，避免冲突。
- **适用场景**：
  - 适合需要图形界面操作的用户，或需要管理复杂依赖关系的场景。
- **安装与使用**：
  - 从官网下载安装包，按向导安装。
  - 通过图形界面或命令行安装软件（如 `npackd install git`）。

### **3. Boxstarter（基于 Chocolatey 的自动化工具）**
- **特点**：
  - **自动化配置**：基于 Chocolatey，支持通过脚本批量安装和配置软件。
  - **环境复现**：可保存当前软件环境配置，快速部署到其他机器。
- **适用场景**：
  - 适合开发者或系统管理员，需要批量部署软件或复现开发环境。
- **安装命令**：
  ```powershell
  # 以管理员身份运行 PowerShell
  . { iwr -useb https://boxstarter.org/bootstrapper.ps1 } | iex; Get-Boxstarter -Force
  ```
- **使用示例**：
  - 创建脚本文件（如 `install.ps1`），编写安装命令，然后通过 Boxstarter 执行。

### **4. Conda（跨平台包管理器）**
- **特点**：
  - **跨平台支持**：支持 Windows、Linux、macOS。
  - **环境隔离**：可创建多个虚拟环境，避免依赖冲突。
  - **科学计算生态**：专注于 Python、R 等科学计算工具管理。
- **适用场景**：
  - 适合数据科学家、机器学习工程师，或需要管理 Python 环境的用户。
- **安装命令**：
  - 从官网下载 Miniconda 或 Anaconda 安装包，按向导安装。
- **使用示例**：
  ```bash
  conda create --name myenv python=3.9  # 创建虚拟环境
  conda activate myenv  # 激活环境
  conda install numpy pandas  # 安装包
  ```

### **5. Pip（Python 包管理器）**
- **特点**：
  - **Python 生态专用**：专注于 Python 库和工具管理。
  - **简单易用**：通过 `pip install` 快速安装包。
- **适用场景**：
  - 适合 Python 开发者，或需要安装 Python 相关工具（如 Jupyter、Scikit-learn）。
- **安装命令**：
  - Python 默认自带 Pip，无需单独安装。
- **使用示例**：
  ```bash
  pip install numpy  # 安装 NumPy
  pip list  # 查看已安装包
  ```

### **6. WingetUI（图形化包管理器）**
- **特点**：
  - **图形界面**：为 Winget、Scoop、Chocolatey 等提供统一 GUI。
  - **多管理器支持**：可同时管理多个包管理器的软件。
- **适用场景**：
  - 适合不喜欢命令行操作的用户，或需要统一管理多个包管理器的场景。
- **安装命令**：
  ```powershell
  winget install SomePythonThings.WingetUIStore  # 通过 Winget 安装
  # 或通过 Scoop 安装
  scoop bucket add extras
  scoop install extras/wingetui
  ```

### **对比与推荐**
| **包管理器** | **类型**       | **优势**                          | **适用场景**                     |
|-------------|---------------|-----------------------------------|----------------------------------|
| **Winget**  | 官方工具       | 集成度高，稳定性强                | 普通用户，管理系统级软件         |
| **Scoop**   | 轻量级工具     | 无需管理员权限，适合开发工具      | 开发者，管理命令行工具           |
| **Npackd**  | 开源工具       | 图形界面，多软件源                | 需要图形化操作的用户             |
| **Boxstarter**| 自动化工具     | 批量部署，环境复现                | 系统管理员，开发者               |
| **Conda**   | 跨平台工具     | 环境隔离，科学计算生态            | 数据科学家，Python 开发者        |
| **Pip**     | Python 专用     | 简单易用，专注 Python 生态        | Python 开发者                    |
| **WingetUI**| 图形化工具     | 统一管理多个包管理器              | 不喜欢命令行的用户               |

### **总结**
- **普通用户**：推荐 **Winget**（官方支持，稳定易用）。
- **开发者**：推荐 **Scoop**（轻量级，适合开发工具） + **Winget**（补充安装 Scoop 没有的软件）。
- **数据科学家**：推荐 **Conda**（环境隔离，科学计算生态）。
- **Python 开发者**：推荐 **Pip**（专注 Python 包管理）。
- **系统管理员**：推荐 **Boxstarter**（批量部署，环境复现）。
- **不喜欢命令行**：推荐 **WingetUI**（图形化统一管理）。



