# 问题、如何安装git?请给出联系的步骤。
# Git 安装与配置步骤

本文详细说明了如何在不同操作系统上安装 Git，并进行基本配置。

---

## 1. Windows 安装步骤

1. **下载 Git 安装包**  
   访问 [Git 官方下载页面](https://git-scm.com/download/win)，下载安装程序。

2. **运行安装程序**  
   双击下载好的 `.exe` 文件，启动安装向导。

3. **按需选择安装选项**  
   一般默认选项即可，点击“下一步”直到“安装”。

4. **完成安装**  
   安装完成后，点击“完成”即可。

5. **验证安装**  
   打开命令提示符（Win + R，输入 `cmd`），输入：
   ```bash
   git --version
   ```
   如果显示 git 版本号，说明安装成功。

---

## 2. macOS 安装步骤

1. **使用 Homebrew 安装（推荐）**  
   如果已安装 Homebrew，打开终端输入：
   ```bash
   brew install git
   ```

2. **或者下载安装包**  
   也可从 [Git 官方下载页面](https://git-scm.com/download/mac)下载安装包并按提示安装。

3. **验证安装**  
   在终端输入：
   ```bash
   git --version
   ```
   出现版本号即安装成功。

---

## 3. Linux 安装步骤（以 Ubuntu 为例）

1. **更新包索引并安装 Git**
   ```bash
   sudo apt update
   sudo apt install git
   ```

2. **验证安装**
   ```bash
   git --version
   ```
   出现版本号即成功。

---

## 4. Git 基本配置（所有平台通用）

安装后建议进行如下基本配置：

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱@example.com"
```

---

## 5. 参考资料

如需更详细的图文教程，可访问 [Git 官方文档](https://git-scm.com/book/zh/v2/起步-安装-Git)。

---

# 如何安装配置 Git-2.50.1-64-bit

以下是安装和配置 Git-2.50.1-64-bit 的详细步骤，涵盖各个选项的用途说明：

#### 一、下载 Git

- **访问官网**：前往 [Git 官方下载页面](https://git-scm.com/download/win)，选择 Windows 系统。
- **选择版本**：下载 64-bit Git for Windows Setup（如 `Git-2.50.1-64-bit.exe`）。

#### 二、安装步骤

1. **运行安装程序**：双击下载的 `Git-2.50.1-64-bit.exe`，启动安装向导。
2. **许可协议**：阅读 GPL 第 2 版协议，点击 Next 继续。
3. **选择安装目录**：
   - **默认路径**：`C:\Program Files\Git`
   - **修改路径**：点击 Browse 选择其他磁盘（如 `D:\Git`），避免中文或空格路径。
   - **用途**：防止因路径问题导致 Git 命令执行异常。
4. **选择安装组件**：
   - **默认勾选**：
     - Git Bash Here：在文件夹右键菜单中添加 Git Bash 快捷方式。
     - Git GUI Here：在文件夹右键菜单中添加 Git GUI 快捷方式。
     - Associate .git files with Git Bash*：关联 .git 文件到 Git Bash。
     - Associate .sh files with Git Bash：关联 .sh 脚本文件到 Git Bash。
   - **可选组件**：
     - Git LFS：处理大文件（如二进制文件）的版本控制。
     - 若需在 Windows 命令行中直接运行 .sh 脚本，可勾选 Associate .sh files with Git Bash。
   - **用途**：根据需求选择是否安装额外功能。
5. **选择开始菜单文件夹**：
   - **默认名称**：Git
   - **修改名称**：点击 Browse 更改文件夹名称或勾选 Don't create a Start Menu folder 跳过。
   - **用途**：管理 Git 相关快捷方式的存放位置。
6. **选择默认编辑器**：
   - **默认选项**：Vim（纯命令行编辑器，操作需学习）。
   - **推荐选项**：
     - Notepad++：轻量级文本编辑器，需提前安装并配置环境变量。
     - Visual Studio Code：功能强大的代码编辑器，支持 Git 集成。
   - **用途**：用于编辑 Git 提交信息、配置文件等。
7. **初始化新仓库的主干分支名称**：
   - **选项 1**：Let Git decide（默认 `master`，未来可能改为 `main`）。
   - **选项 2**：Override the default branch name for new repositories（自定义名称，如 `main`）。
   - **用途**：适应团队协作或项目规范要求。
8. **调整 PATH 环境变量**：
   - **选项 1**：Use Git from Git Bash only
     - **用途**：仅在 Git Bash 中使用 Git，不修改系统 PATH，避免与其他工具冲突。
   - **选项 2**：Git from the command line and also from 3rd-party software（推荐）
     - **用途**：允许在 Git Bash、命令提示符（CMD）、PowerShell 及第三方软件中使用 Git。
   - **选项 3**：Use Git and optional Unix tools from the Command Prompt
     - **用途**：将 Git 和 Unix 工具（如 `find`、`sort`）添加到 PATH，但可能覆盖 Windows 原生工具。
9. **选择 SSH 执行文件**：
   - **默认选项**：Use bundled OpenSSH
     - **用途**：使用 Git 自带的 OpenSSH 客户端进行安全连接。
10. **选择 HTTPS 后端传输**：
    - **默认选项**：Use the native Windows Secure Channel library
      - **用途**：利用 Windows 自带的加密库进行 HTTPS 传输，兼容性更好。
11. **配置行尾符号转换**：
    - **选项 1**：Checkout Windows-style, commit Unix-style line endings（推荐）
      - **用途**：在 Windows 上检出文件时使用 CRLF，提交时转换为 LF，避免跨平台协作时的换行符冲突。
    - **选项 2**：Checkout as-is, commit Unix-style line endings
      - **用途**：检出时不转换行尾符号，提交时统一为 LF。
12. **配置终端模拟器**：
    - **默认选项**：Use MinTTY (the default terminal of MSYS2)
      - **用途**：使用 MinTTY 作为终端，支持 Unicode 和 256 色，但与 Windows 命令行工具兼容性较差。
    - **选项 2**：Use Windows' default console window
      - **用途**：使用 Windows 原生命令提示符，兼容性更好，但功能较少。
13. **选择 git pull 默认行为**：
    - **默认选项**：Fast-forward or merge
      - **用途**：自动合并远程更改到本地分支。
    - **选项 2**：Rebase
      - **用途**：将本地更改“变基”到远程分支最新提交之后，保持提交历史线性。
14. **选择凭据管理器**：
    - **默认选项**：Git Credential Manager Core
      - **用途**：跨平台凭据管理器，支持 Windows、macOS 和 Linux，方便存储和访问代码托管平台（如 GitHub）的凭据。
15. **配置实验性选项**：
    - **默认选项**：不勾选
      - **用途**：避免使用尚未稳定的实验性功能。
16. **开始安装**：点击 Install，等待安装完成。
17. **完成安装**：勾选 Launch Git Bash 和 View Release Notes（可选），点击 Finish。

#### 三、验证安装

- **打开 Git Bash**：在开始菜单或桌面快捷方式中启动 Git Bash。
- **检查版本**：输入命令 `git --version`，输出示例：`git version 2.50.1.windows.1`。

#### 四、基本配置

- **设置用户名和邮箱**：
  - 输入命令（替换为你的信息）：
    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"
    ```
  - **用途**：标识代码提交的作者身份。
- **查看配置**：输入命令 `git config --list`，确认输出中包含 `user.name` 和 `user.email`。

#### 五、可选配置

- **配置 SSH 密钥（推荐）**：
  - 生成 SSH 密钥并添加到 GitHub/GitLab：
    ```bash
    ssh-keygen -t ed25519 -C "your.email@example.com"
    cat ~/.ssh/id_ed25519.pub
    ```
  - 将公钥粘贴到代码托管平台的 SSH Keys 设置中。
- **配置代理（如需）**：
  - 若需通过代理访问网络：
    ```bash
    git config --global http.proxy http://proxy.example.com:8080
    git config --global https.proxy https://proxy.example.com:8080
    ```

# 如何安装配置 GitHub Hub

GitHub Hub 是 GitHub 的命令行工具，用于简化 Git 操作（如克隆仓库、创建 Pull Request 等）。以下是安装和配置 GitHub Hub 的详细步骤：

#### 一、安装 GitHub Hub

1. **使用 Scoop 安装（推荐）**：
   - **步骤 1**：以管理员身份打开 PowerShell，运行以下命令以允许执行远程脚本：
     ```powershell
     Set-ExecutionPolicy RemoteSigned -scope CurrentUser
     ```
   - **步骤 2**：安装 Scoop（若未安装）：
     ```powershell
     iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
     ```
   - **步骤 3**：安装 GitHub Hub：
     ```powershell
     scoop install hub
     ```
2. **手动安装**：
   - **步骤 1**：从 [GitHub Hub Releases](https://github.com/github/hub/releases) 下载适用于您操作系统的二进制文件。
   - **步骤 2**：解压文件，并将 `hub.exe`（Windows）或 `hub`（Linux/macOS）复制到系统环境变量 PATH 包含的目录中（如 `/usr/local/bin`）。
3. **验证安装**：
   - 打开终端（Git Bash、CMD 或 PowerShell），运行以下命令：
     ```bash
     hub version
     ```
   - 输出示例：
     ```
     git version 2.50.1.windows.1
     hub version 2.14.0
     ```

#### 二、配置 GitHub Hub

安装完成后，需配置 GitHub 凭据以实现身份验证。

1. **配置 SSH 密钥（推荐）**：
   - **步骤 1**：生成 SSH 密钥（若未生成）：
     ```bash
     ssh-keygen -t ed25519 -C "your.email@example.com"
     ```
     按提示操作，默认路径为 `~/.ssh/id_ed25519.pub`（Linux/macOS）或 `C:\Users\YourName\.ssh\id_ed25519.pub`（Windows）。
   - **步骤 2**：将公钥添加到 GitHub：
     ```bash
     cat ~/.ssh/id_ed25519.pub # Linux/macOS
     type C:\Users\YourName\.ssh\id_ed25519.pub # Windows
     ```
     登录 GitHub，进入 Settings → SSH and GPG Keys → New SSH Key，粘贴公钥并保存。
2. **配置 HTTPS 凭据存储（替代方案）**：
   - **步骤 1**：配置 Git 全局凭据管理器（Windows）：
     ```bash
     git config --global credential.helper manager
     ```
   - **步骤 2**：首次执行 `hub clone` 或 `git push` 时，会弹出窗口要求输入 GitHub 用户名和密码（或 Personal Access Token）。
3. **配置 GitHub Hub 全局选项**：
   - **步骤 1**：设置 GitHub 主机别名（可选）：
     ```bash
     git config --global hub.host github.com
     ```
     **用途**：指定 Hub 操作的 GitHub 主机（默认即为 `github.com`）。
   - **步骤 2**：配置协议（可选）：
     ```bash
     git config --global hub.protocol https
     ```
     **用途**：强制使用 HTTPS 协议（默认根据仓库 URL 自动选择）。

#### 三、基本用法与选项说明

GitHub Hub 扩展了 Git 命令，以下为常用命令及选项：

1. **克隆仓库**：
   - `hub clone owner/repo`
     - **用途**：克隆指定用户的仓库（等价于 `git clone git@github.com:owner/repo.git`）。
     - **选项**：
       - `-p`：使用 HTTPS 协议（默认 SSH）。
       - `-h`：显示帮助信息。
2. **创建 Pull Request**：
   - `hub pull-request -m "Title" -b "owner:branch" -r "reviewer1,reviewer2"`
     - **用途**：从当前分支创建 Pull Request 到目标分支。
     - **选项**：
       - `-m`：指定 PR 标题。
       - `-b`：指定目标分支（格式为 `owner:branch`）。
       - `-r`：指定审阅人（逗号分隔）。
       - `-f`：强制推送（覆盖现有 PR）。
3. **浏览仓库**：
   - `hub browse`
     - **用途**：在默认浏览器中打开当前仓库的 GitHub 页面。
     - **选项**：
       - `--issues`：打开 Issues 页面。
       - `--pulls`：打开 Pull Requests 页面。
4. **创建仓库**：
   - `hub create -p -d "Description" -h "Homepage"`
     - **用途**：在 GitHub 上创建新仓库并初始化本地 Git 仓库。
     - **选项**：
       - `-p`：设置为私有仓库。
       - `-d`：指定仓库描述。
       - `-h`：指定仓库主页 URL。
5. **对比分支**：
   - `hub compare branch1...branch2`
     - **用途**：在浏览器中打开两个分支的对比页面。

#### 四、高级配置

1. **使用 Personal Access Token（PAT）**：
   - 若未配置 SSH 密钥，可通过 PAT 进行身份验证：

---

# GitHub Hub 安装与配置详尽指南

## 一、安装 GitHub Hub

GitHub Hub 是 GitHub 的命令行工具，用于简化 Git 操作（如克隆仓库、创建 Pull Request 等）。以下是安装步骤：

### 1. 使用 Scoop 安装（推荐）

- **步骤 1**：以管理员身份打开 PowerShell，运行以下命令以允许执行远程脚本：
  ```powershell
  Set-ExecutionPolicy RemoteSigned -scope CurrentUser
  ```
- **步骤 2**：安装 Scoop（若未安装）：
  ```powershell
  iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
  ```
- **步骤 3**：安装 GitHub Hub：
  ```powershell
  scoop install hub
  ```

### 2. 手动安装

- **步骤 1**：从 [GitHub Hub Releases](https://github.com/github/hub/releases) 下载适用于您操作系统的二进制文件。
- **步骤 2**：解压文件，并将 `hub.exe`（Windows）或 `hub`（Linux/macOS）复制到系统环境变量 PATH 包含的目录中（如 `/usr/local/bin`）。

### 3. 验证安装

打开终端（Git Bash、CMD 或 PowerShell），运行以下命令：
```bash
hub version
```
输出示例：
```
git version 2.50.1.windows.1
hub version 2.14.0
```

## 二、配置 GitHub Hub

安装完成后，需配置 GitHub 凭据以实现身份验证。

### 1. 配置 SSH 密钥（推荐）

- **步骤 1**：生成 SSH 密钥（若未生成）：
  ```bash
  ssh-keygen -t ed25519 -C "your.email@example.com"
  ```
  按提示操作，默认路径为 `~/.ssh/id_ed25519.pub`（Linux/macOS）或 `C:\Users\YourName\.ssh\id_ed25519.pub`（Windows）。

- **步骤 2**：将公钥添加到 GitHub：
  复制公钥内容：
  ```bash
  cat ~/.ssh/id_ed25519.pub # Linux/macOS
  type C:\Users\YourName\.ssh\id_ed25519.pub # Windows
  ```
  登录 GitHub，进入 `Settings` → `SSH and GPG Keys` → `New SSH Key`，粘贴公钥并保存。

### 2. 配置 HTTPS 凭据存储（替代方案）

- **步骤 1**：配置 Git 全局凭据管理器（Windows）：
  ```bash
  git config --global credential.helper manager
  ```
- **步骤 2**：首次执行 `hub clone` 或 `git push` 时，会弹出窗口要求输入 GitHub 用户名和密码（或 Personal Access Token）。

### 3. 配置 GitHub Hub 全局选项

- **步骤 1**：设置 GitHub 主机别名（可选）：
  ```bash
  git config --global hub.host github.com
  ```
  **用途**：指定 Hub 操作的 GitHub 主机（默认即为 github.com）。

- **步骤 2**：配置协议（可选）：
  ```bash
  git config --global hub.protocol https
  ```
  **用途**：强制使用 HTTPS 协议（默认根据仓库 URL 自动选择）。

## 三、基本用法与选项说明

GitHub Hub 扩展了 Git 命令，以下为常用命令及选项：

### 1. 克隆仓库

```bash
hub clone owner/repo
```
**用途**：克隆指定用户的仓库（等价于 `git clone git@github.com:owner/repo.git`）。

**选项**：
- `-p`：使用 HTTPS 协议（默认 SSH）。
- `-h`：显示帮助信息。

### 2. 创建 Pull Request

```bash
hub pull-request -m "Title" -b "owner:branch" -r "reviewer1,reviewer2"
```
**用途**：从当前分支创建 Pull Request 到目标分支。

**选项**：
- `-m`：指定 PR 标题。
- `-b`：指定目标分支（格式为 `owner:branch`）。
- `-r`：指定审阅人（逗号分隔）。
- `-f`：强制推送（覆盖现有 PR）。

### 3. 浏览仓库

```bash
hub browse
```
**用途**：在默认浏览器中打开当前仓库的 GitHub 页面。

**选项**：
- `--issues`：打开 Issues 页面。
- `--pulls`：打开 Pull Requests 页面。

### 4. 创建仓库

```bash
hub create -p -d "Description" -h "Homepage"
```
**用途**：在 GitHub 上创建新仓库并初始化本地 Git 仓库。

**选项**：
- `-p`：设置为私有仓库。
- `-d`：指定仓库描述。
- `-h`：指定仓库主页 URL。

### 5. 对比分支

```bash
hub compare branch1...branch2
```
**用途**：在浏览器中打开两个分支的对比页面。

## 四、高级配置

### 1. 使用 Personal Access Token（PAT）

若未配置 SSH 密钥，可通过 PAT 进行身份验证：
登录 GitHub，进入 `Settings` → `Developer settings` → `Personal access tokens` → `Tokens (classic)` → `Generate new token`。
勾选 `repo` 和 `user` 权限，生成 Token。
在终端中运行：
```bash
git config --global github.token YOUR_TOKEN
```

### 2. 配置代理（适用于国内用户）

```bash
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy http://127.0.0.1:1080
```
**用途**：通过代理加速 GitHub 访问。

## 五、常见问题解决

- **hub version 报错**：
  - 检查 `hub.exe` 是否在 PATH 中。
  - 重新启动终端或运行 `source ~/.bashrc`（Linux/macOS）。

- **SSH 连接失败**：
  - 确保 SSH 密钥已添加到 GitHub。
  - 运行 `ssh -T git@github.com` 测试连接。

- **HTTPS 凭据提示频繁出现**：
  - 使用 PAT 替代密码。
  - 或运行 `git config --global credential.helper store` 永久保存凭据（不推荐，存在安全风险）。

---

# GitHub Hub 安装与配置指南（SSH 协议优先）

## 一、安装 GitHub Hub

GitHub Hub 是 GitHub 的命令行工具，扩展了 Git 命令的功能（如快速创建 PR、克隆仓库等）。以下是安装步骤：

### 1. 使用 Scoop 安装（Windows 推荐）

```powershell
# 允许执行远程脚本（仅首次需要）
Set-ExecutionPolicy RemoteSigned -scope CurrentUser
# 安装 Scoop
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
# 安装 GitHub Hub
scoop install hub
```

### 2. 手动安装

- **Linux/macOS**：从 GitHub Hub Releases 下载二进制文件，解压后将 `hub` 复制到 `/usr/local/bin`。
- **Windows**：下载 `hub.exe` 并添加到系统 PATH 环境变量。

### 3. 验证安装

```bash
hub version
```

输出示例：

```bash
git version 2.50.1.windows.1
hub version 2.14.0
```

## 二、配置 SSH 凭据（推荐）

GitHub 已弃用密码认证，推荐使用 SSH 协议。以下是配置步骤：

### 1. 生成 SSH 密钥

```bash
ssh-keygen -t ed25519 -C "your.email@example.com"
```

**选项说明**：
- `-t ed25519`：指定密钥类型（更安全且高效）。
- `-C`：添加注释（通常为邮箱）。

**操作提示**：
- 按提示输入保存路径（默认 `~/.ssh/id_ed25519`）。
- 可设置密码（留空则无密码）。

### 2. 添加 SSH 密钥到 GitHub

```bash
# 查看公钥内容
cat ~/.ssh/id_ed25519.pub
```

复制输出内容，登录 GitHub → Settings → SSH and GPG Keys → New SSH Key，粘贴并保存。

### 3. 测试 SSH 连接

```bash
ssh -T git@github.com
```

成功输出：

```bash
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

### 4. 多账号 SSH 配置（高级）

若需管理多个 GitHub 账号，编辑 `~/.ssh/config` 文件：

```bash
# 个人账号
Host personal.github.com
 HostName github.com
 User git
 IdentityFile ~/.ssh/id_ed25519_personal
# 工作账号
Host work.github.com
 HostName github.com
 User git
 IdentityFile ~/.ssh/id_ed25519_work
```

**用途**：通过不同 Host 别名区分账号，避免密钥冲突。

## 三、配置 GitHub Hub 全局选项

编辑 `~/.gitconfig` 文件（或通过命令行配置）：

```bash
# 设置 GitHub 主机别名（默认无需修改）
git config --global hub.host github.com
# 强制使用 SSH 协议（覆盖仓库默认协议）
git config --global hub.protocol ssh
```

**选项说明**：
- `hub.host`：指定 Hub 操作的 GitHub 主机（默认 github.com）。
- `hub.protocol`：强制使用 SSH 协议（避免 HTTPS 提示输入密码）。

## 四、配置 HTTPS 凭据存储（替代方案）

若无法使用 SSH，可通过 HTTPS 凭据管理器存储密码（不推荐，安全性较低）：

### 1. 配置 Git 凭据管理器

```bash
# Windows
git config --global credential.helper manager
# macOS
git config --global credential.helper osxkeychain
# Linux
git config --global credential.helper cache --timeout=3600
```

**选项说明**：
- `manager`：Windows 凭据管理器。
- `osxkeychain`：macOS 钥匙串。
- `cache`：临时缓存凭据（默认 15 分钟，`--timeout` 可修改）。

### 2. 首次推送时输入凭据

```bash
git push origin main
```

系统会弹出窗口要求输入 GitHub 用户名和密码（或 Personal Access Token）。

## 五、使用 GitHub Hub 常用命令

### 1. 克隆仓库

```bash
hub clone owner/repo
```

**用途**：等价于 `git clone git@github.com:owner/repo.git`（使用 SSH）。

### 2. 创建 Pull Request

```bash
hub pull-request -m "Title" -b "owner:branch" -r "reviewer1,reviewer2"
```

**选项说明**：
- `-m`：指定 PR 标题。
- `-b`：目标分支（格式 `owner:branch`）。
- `-r`：指定审阅人（逗号分隔）。

### 3. 浏览仓库

```bash
hub browse
```

**选项说明**：
- `--issues`：打开 Issues 页面。
- `--pulls`：打开 Pull Requests 页面。

## 六、常见问题解决

### hub version 报错

- 检查 `hub` 是否在 PATH 中。
- 重新启动终端或运行 `source ~/.bashrc`（Linux/macOS）。

### SSH 连接失败

- 确保 SSH 密钥已添加到 GitHub。
- 运行 `ssh -T git@github.com` 测试连接。

### HTTPS 凭据频繁提示

- 使用 Personal Access Token（PAT）替代密码：
  - 登录 GitHub → Settings → Developer settings → Personal access tokens → Generate new token。
  - 勾选 `repo` 和 `user` 权限，生成 Token。
  - 运行 `git config --global github.token YOUR_TOKEN` 存储 Token。

---

# 如何安装配置 GitHub gh

### **GitHub `gh` 命令行工具安装与配置指南（2025 年最新版，附扩展配置）**

#### **一、安装 `gh` 工具**
`gh` 是 GitHub 官方推出的命令行工具，支持代码托管、Issue 管理、PR 操作等核心功能。以下是安装方法：

1. **macOS/Linux**  
   使用 Homebrew 或系统包管理器安装：
   ```bash
   # macOS（推荐）
   brew install gh

   # Linux（如 Ubuntu/Debian）
   sudo apt-get install gh
   ```

2. **Windows**  
   通过 [GitHub CLI 发布页](https://github.com/cli/cli/releases) 下载 MSI 安装包，或使用 Chocolatey：
   ```powershell
   choco install gh
   ```

3. **手动安装（通用）**  
   下载对应系统的二进制文件，移动到系统路径（如 `/usr/local/bin` 或 `%PATH%` 目录）：
   ```bash
   # 示例：Linux/macOS 手动安装
   wget https://github.com/cli/cli/releases/download/v2.64.0/gh_2.64.0_linux_amd64.tar.gz
   tar -xzf gh_*.tar.gz
   sudo mv gh_*/bin/gh /usr/local/bin/
   ```

#### **二、登录 GitHub 账号**
安装完成后，需通过以下命令登录账号以授权操作：
```bash
gh auth login
```
按提示选择登录方式：
1. **认证方式**：
   - **HTTPS**：推荐，需输入账号密码（支持 Token 输入）。
   - **SSH**：需提前配置 SSH 密钥（通过 `ssh-keygen` 生成并添加到 GitHub）。
2. **登录范围**：
   - `github.com`：适用于公共 GitHub。
   - 企业版 GitHub：需输入域名（如 `github.example.com`）。
3. **权限范围**：
   - **Read and Write**：支持完整功能（如创建 PR、管理 Issue）。
   - **Read Only**：仅查看权限。
4. **验证方式**：
   - **Web 浏览器**：打开生成的 URL 扫码或授权（推荐）。
   - **Token 输入**：在 GitHub [Personal Access Tokens](https://github.com/settings/tokens) 页面生成 Token 后粘贴。

#### **三、基础配置**
1. **全局配置**  
   设置默认编辑器、Git 用户信息等：
   ```bash
   # 设置默认编辑器（如 VSCode）
   gh config set editor "code --wait"

   # 设置 Git 协议（HTTPS 或 SSH）
   gh config set git_protocol ssh

   # 查看当前配置
   gh config get
   ```

2. **仓库级配置**  
   进入项目目录后，可针对单个仓库配置：
   ```bash
   cd /path/to/repo
   gh repo view --web  # 在浏览器打开仓库页面
   gh issue create --title "New Issue" --body "Issue details"  # 创建 Issue
   ```

#### **四、常用功能示例**
1. **克隆仓库**  
   ```bash
   gh repo clone github/gh-skyline  # 克隆 GitHub 官方示例项目
   ```

2. **管理 Issue/PR**  
   ```bash
   gh issue list                     # 列出当前仓库 Issue
   gh issue create --fill             # 基于未提交更改创建 Issue
   gh pr create --fill                # 创建 PR（自动填充标题和描述）
   gh pr checkout 123                # 检出 PR #123 到本地分支
   gh pr merge 123 --merge            # 合并 PR（支持 --squash 或 --rebase）
   ```

3. **生成 GitHub 贡献 3D 图**  
   使用 `gh-skyline` 扩展（需提前安装）：
   ```bash
   # 安装扩展
   gh extension install github/gh-skyline

   # 生成 2024 年贡献图
   gh skyline --year 2024 --output skyline.png

   # 参数说明：
   # --year: 指定年份（默认当前年）
   # --output: 输出文件路径
   ```

4. **企业版 GitHub 支持**  
   若使用 GitHub Enterprise，需在登录时指定域名：
   ```bash
   gh auth login --hostname github.example.com --web
   ```

#### **五、扩展推荐与配置**
1. **`gh-dash`：命令行仪表盘**  
   实时展示 PR/Issue 状态，支持自定义过滤和快捷键：
   ```bash
   # 安装
   gh extension install dlvhdr/gh-dash

   # 启动仪表盘
   gh dash

   # 常用命令：
   # --filter "state:open author:@me"  # 过滤当前用户的开放 PR
   # --sort updated                    # 按更新时间排序
   ```

2. **`gh-api`：直接调用 GitHub API**  
   ```bash
   # 安装
   gh extension install fastai/ghapi

   # 示例：列出所有 Issue 标题
   gh api repos/github/gh/issues --paginate | jq '.[].title'
   ```

3. **`gh-find-current-pr`：查找当前分支的 PR**  
   ```bash
   # 安装
   npm install -g gh-find-current-pr

   # 使用
   gh-find-current-pr
   ```

#### **六、故障排查**
1. **权限错误**  
   - 确保 Token 或 SSH 密钥具有足够权限（如 `repo` 范围）。
   - 检查 `~/.config/gh/hosts.yml` 是否配置了企业版域名。

2. **网络问题**  
   - 代理设置：
     ```bash
     gh config set http_proxy "http://proxy.example.com:8080"
     ```
   - 验证网络连通性：
     ```bash
     gh api /user --include  # 测试 API 访问
     ```

3. **版本升级**  
   ```bash
   # macOS/Linux
   brew upgrade gh

   # Windows
   choco upgrade gh
   ```

#### **七、完整配置示例**
```bash
# 1. 安装 gh
brew install gh

# 2. 登录 GitHub
gh auth login --web

# 3. 全局配置
gh config set editor "code --wait"
gh config set git_protocol ssh

# 4. 安装扩展
gh extension install github/gh-skyline
gh extension install dlvhdr/gh-dash

# 5. 生成贡献图
gh skyline --year 2024 --output ~/Desktop/skyline.png

# 6. 启动仪表盘
gh dash --filter "state:open label:bug"
```

### **总结**
- **安装**：优先选择包管理器（Homebrew/apt/choco），手动安装作为备选。
- **登录**：推荐 Token 或 SSH 方式，企业版需配置域名。
- **配置**：全局设置编辑器、协议，仓库级操作直接调用 `gh` 命令。
- **扩展**：根据需求安装 `gh-skyline`、`gh-dash` 等增强功能。

通过以上步骤，您可快速上手 `gh` 工具，高效管理 GitHub 项目。如遇问题，可运行 `gh help` 查看内置文档或访问 [GitHub CLI 官方文档](https://cli.github.com/manual/)。

---

# 如何安装配置github gh，请给出最为详尽的安装配置步骤和方法并一一列出各个选项并说明它们各自的用途。

### **GitHub `gh` 命令行工具安装与配置指南（2025 年最新版）**

#### **一、安装 `gh` 工具**
`gh` 是 GitHub 官方推出的命令行工具，支持代码托管、Issue 管理、PR 操作等核心功能。以下是安装方法：

1. **macOS/Linux**  
   使用 Homebrew 或系统包管理器安装：
   ```bash
   # macOS（推荐）
   brew install gh

   # Linux（如 Ubuntu/Debian）
   sudo apt-get install gh

   # 验证安装
   gh --version
   ```

2. **Windows**  
   通过 [GitHub CLI 发布页](https://github.com/cli/cli/releases) 下载 MSI 安装包，或使用 Chocolatey：
   ```powershell
   choco install gh
   ```

3. **手动安装（通用）**  
   下载对应系统的二进制文件，移动到系统路径（如 `/usr/local/bin` 或 `%PATH%` 目录）：
   ```bash
   # 示例：Linux/macOS 手动安装
   wget https://github.com/cli/cli/releases/download/v2.64.0/gh_2.64.0_linux_amd64.tar.gz
   tar -xzf gh_*.tar.gz
   sudo mv gh_*/bin/gh /usr/local/bin/
   ```

#### **二、登录 GitHub 账号**
安装完成后，需通过以下命令登录账号以授权操作：
```bash
gh auth login
```
按提示选择登录方式：
1. **选择认证方式**：推荐 `HTTPS`（需输入账号密码）或 `SSH`（需提前配置密钥）。
2. **登录范围**：根据需求选择 `github.com` 或企业版 GitHub。
3. **权限范围**：建议选择 `Read and Write` 以支持完整功能。
4. **验证方式**：
   - **Web 浏览器**：打开生成的 URL 扫码或授权。
   - **Token 输入**：在 GitHub [Personal Access Tokens](https://github.com/settings/tokens) 页面生成 Token 后粘贴。

#### **三、基础配置**
1. **全局配置**  
   设置默认编辑器、Git 用户信息等：
   ```bash
   # 设置默认编辑器（如 VSCode）
   gh config set editor "code --wait"

   # 设置 Git 用户信息（与 git config 同步）
   gh config set git_protocol ssh
   ```

2. **仓库级配置**  
   进入项目目录后，可针对单个仓库配置：
   ```bash
   cd /path/to/repo
   gh repo view --web  # 在浏览器打开仓库页面
   gh issue create --title "New Issue" --body "Issue details"  # 创建 Issue
   ```

#### **四、常用功能示例**
1. **克隆仓库**  
   ```bash
   gh repo clone github/gh-skyline  # 克隆 GitHub 官方示例项目
   ```

2. **管理 Issue/PR**  
   ```bash
   gh issue list                     # 列出当前仓库 Issue
   gh pr create --fill               # 基于未提交更改创建 PR
   gh pr checkout 123                # 检出 PR #123 到本地分支
   ```

3. **生成 GitHub 贡献 3D 图**  
   使用 `gh-skyline` 扩展（需提前安装）：
   ```bash
   gh extension install github/gh-skyline
   gh skyline --year 2024 --output skyline.png  # 生成 2024 年贡献图
   ```

4. **企业版 GitHub 支持**  
   若使用 GitHub Enterprise，需在登录时指定域名：
   ```bash
   gh auth login --hostname github.example.com --web
   ```

#### **五、故障排查**
1. **权限错误**  
   - 确保 Token 或 SSH 密钥具有足够权限（如 `repo` 范围）。
   - 检查 `~/.config/gh/hosts.yml` 是否配置了企业版域名。

2. **网络问题**  
   - 代理设置：
     ```bash
     gh config set http_proxy "http://proxy.example.com:8080"
     ```
   - 验证网络连通性：
     ```bash
     gh api /user --include  # 测试 API 访问
     ```

3. **版本升级**  
   ```bash
   # macOS/Linux
   brew upgrade gh

   # Windows
   choco upgrade gh
   ```

#### **六、扩展推荐**
1. **`gh-dash`**：命令行仪表盘，实时展示 PR/Issue 状态。
   ```bash
   gh extension install dlvhdr/gh-dash
   gh dash  # 启动仪表盘
   ```

2. **`gh-api`**：直接调用 GitHub API。
   ```bash
   gh extension install fastai/ghapi
   gh api repos/github/gh/issues --paginate | jq '.[].title'  # 列出所有 Issue 标题
   ```

### **总结**
- **安装**：优先选择包管理器（Homebrew/apt/choco），手动安装作为备选。
- **登录**：推荐 Token 或 SSH 方式，企业版需配置域名。
- **配置**：全局设置编辑器、协议，仓库级操作直接调用 `gh` 命令。
- **扩展**：根据需求安装 `gh-skyline`、`gh-dash` 等增强功能。

通过以上步骤，您可快速上手 `gh` 工具，高效管理 GitHub 项目。如遇问题，可运行 `gh help` 查看内置文档或访问 [GitHub CLI 官方文档](https://cli.github.com/manual/)。
