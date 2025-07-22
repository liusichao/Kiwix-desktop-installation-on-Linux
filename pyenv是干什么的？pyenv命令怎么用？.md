# pyenv是干什么的？
## pyenv命令怎么用？

### **Pyenv 的作用**
Pyenv 是一个用于管理多个 Python 版本的工具，它允许开发者在同一台机器上轻松安装、切换和管理不同版本的 Python。Pyenv 的核心功能包括：
1. **多版本管理**：可以安装和管理多个 Python 版本（包括官方版本、Anaconda、PyPy 等）。
2. **版本切换**：支持全局、局部（项目级）和临时（Shell 会话级）的 Python 版本切换。
3. **环境隔离**：通过与虚拟环境工具（如 `pyenv-virtualenv`）结合，可以为不同项目创建独立的 Python 环境，避免依赖冲突。

Pyenv 的优势在于它不会修改系统级的 Python 安装，而是通过修改 `PATH` 环境变量和创建 shim 文件（代理脚本）来动态切换 Python 版本。

---

### **Pyenv 常用命令**
以下是 Pyenv 的常用命令及其用法：

#### 1. **安装 Python 版本**
```bash
# 查看可安装的 Python 版本
pyenv install --list

# 安装指定版本的 Python（例如 3.9.7）
pyenv install 3.9.7

# 安装最新版本的 Python（例如 3.x 的最新稳定版）
pyenv install $(pyenv latest 3)
```

#### 2. **查看已安装的 Python 版本**
```bash
# 查看所有已安装的 Python 版本
pyenv versions

# 查看当前使用的 Python 版本
pyenv version
```

#### 3. **切换 Python 版本**
Pyenv 支持三种级别的版本切换：
- **全局切换**（影响整个系统）：
  ```bash
  pyenv global 3.9.7  # 设置全局默认版本为 3.9.7
  ```
- **局部切换**（仅对当前目录及其子目录生效）：
  ```bash
  pyenv local 3.8.12  # 在当前目录下创建 .python-version 文件，指定版本为 3.8.12
  pyenv local --unset  # 取消局部版本设置
  ```
- **临时切换**（仅对当前 Shell 会话生效）：
  ```bash
  pyenv shell 3.7.9  # 在当前 Shell 会话中临时使用 3.7.9
  pyenv shell --unset  # 取消临时版本设置
  ```

#### 4. **卸载 Python 版本**
```bash
pyenv uninstall 3.9.7  # 卸载指定版本的 Python
```

#### 5. **其他实用命令**
```bash
# 重新生成 shim 文件（安装新版本或包后需要执行）
pyenv rehash

# 查看命令的实际执行路径
pyenv which python  # 例如输出：/home/user/.pyenv/versions/3.9.7/bin/python

# 查找安装了特定命令的所有 Python 版本
pyenv whence pip  # 例如输出：3.8.12 3.9.7
```

#### 6. **与虚拟环境结合使用**
Pyenv 可以与 `pyenv-virtualenv` 插件结合，为不同项目创建独立的虚拟环境：
```bash
# 安装 pyenv-virtualenv 插件
git clone https://github.com/pyenv/pyenv-virtualenv.git $(pyenv root)/plugins/pyenv-virtualenv

# 在 shell 配置文件中添加初始化（如 ~/.bashrc）
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.bashrc
source ~/.bashrc

# 创建虚拟环境
pyenv virtualenv 3.9.7 myenv  # 基于 Python 3.9.7 创建名为 myenv 的虚拟环境

# 激活虚拟环境
pyenv activate myenv

# 停用虚拟环境
pyenv deactivate

# 删除虚拟环境
pyenv uninstall myenv
```

---

### **Pyenv 的工作原理**
Pyenv 通过以下方式实现版本管理：
1. **修改 PATH**：将 `~/.pyenv/shims` 目录添加到 `PATH` 的最前面，Pyenv 会在该目录下创建所有已安装 Python 版本的 shim 文件（代理脚本）。
2. **版本选择**：Pyenv 按照以下优先级顺序选择 Python 版本：
   - `PYENV_VERSION` 环境变量
   - 当前目录下的 `.python-version` 文件（由 `pyenv local` 创建）
   - 父目录中的 `.python-version` 文件（递归查找）
   - 全局版本（由 `pyenv global` 设置）
3. **Shim 文件**：当用户运行 `python` 或 `pip` 等命令时，Pyenv 会通过 shim 文件动态调用指定版本的 Python。

---

### **安装 Pyenv**
#### 1. **Linux/macOS 安装**
```bash
# 使用 curl 安装
curl https://pyenv.run | bash

# 在 shell 配置文件中添加初始化（如 ~/.bashrc）
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
source ~/.bashrc
```

#### 2. **Windows 安装**
Windows 用户可以使用 `pyenv-win`：
```bash
# 使用 Chocolatey 安装（推荐）
choco install pyenv-win

# 或者手动安装
git clone https://github.com/pyenv-win/pyenv-win.git "%USERPROFILE%\.pyenv"
```

---

### **总结**
Pyenv 是一个功能强大的 Python 版本管理工具，适合需要同时使用多个 Python 版本的开发者。通过 Pyenv，你可以轻松安装、切换和管理不同版本的 Python，并结合虚拟环境工具实现项目间的环境隔离。掌握 Pyenv 的常用命令可以大大提高开发效率，避免版本冲突问题。
