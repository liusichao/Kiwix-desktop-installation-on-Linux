# 如何用pyenv查询Python版本？
## 使用 `pyenv` 查询已安装的 Python 版本或可用的 Python 版本非常简单，以下是详细的操作指南：

---

### **1. 查询已安装的 Python 版本**
使用 `pyenv versions` 命令可以列出当前环境中已安装的所有 Python 版本（包括全局版本、本地版本和 shell 版本）。

```bash
pyenv versions
```

**输出示例**：
```
  system
* 3.8.12 (set by /home/user/.python-version)
  3.9.7
  3.10.0
```
- `system` 表示系统自带的 Python 版本（未通过 `pyenv` 安装）。
- `*` 表示当前激活的 Python 版本。
- 其他版本是用户通过 `pyenv` 安装的。

---

### **2. 查询可安装的 Python 版本**
使用 `pyenv install --list` 命令可以列出所有可通过 `pyenv` 安装的 Python 版本（包括正式版、预发布版等）。

```bash
pyenv install --list
```

**输出示例（部分）**：
```
Available versions:
  2.7.18
  3.5.10
  3.6.15
  3.7.12
  3.8.12
  3.9.7
  3.10.0
  3.11-dev
  pypy2.7-7.3.7
  pypy3.8-7.3.7
```
- 版本号前面的 `pypy` 表示 PyPy（Python 的替代实现）。
- 版本号带 `-dev` 表示开发版本（可能不稳定）。

---

### **3. 查询当前激活的 Python 版本**
使用 `pyenv version` 命令可以查看当前 shell 会话中激活的 Python 版本。

```bash
pyenv version
```

**输出示例**：
```
3.8.12 (set by /home/user/.python-version)
```
- 显示当前激活的版本及其来源（如 `.python-version` 文件）。

---

### **4. 查询全局 Python 版本**
使用 `pyenv global` 命令可以查看或设置全局 Python 版本（影响所有新打开的 shell 会话）。

**查看全局版本**：
```bash
pyenv global
```

**设置全局版本（例如设置为 3.9.7）**：
```bash
pyenv global 3.9.7
```

---

### **5. 查询本地 Python 版本（针对特定目录）**
使用 `pyenv local` 命令可以查看或设置当前目录及其子目录的 Python 版本。

**查看本地版本**：
```bash
pyenv local
```

**设置本地版本（例如设置为 3.10.0）**：
```bash
pyenv local 3.10.0
```
- 会在当前目录下生成一个 `.python-version` 文件，记录本地版本。

---

### **6. 查询 Shell 特定的 Python 版本**
使用 `pyenv shell` 命令可以临时设置当前 shell 会话的 Python 版本（不影响其他会话）。

**查看 Shell 版本**：
```bash
pyenv shell
```

**设置 Shell 版本（例如设置为 3.8.12）**：
```bash
pyenv shell 3.8.12
```

---

### **总结**
- `pyenv versions`：列出所有已安装的版本。
- `pyenv install --list`：列出所有可安装的版本。
- `pyenv version`：查看当前激活的版本。
- `pyenv global`：查看或设置全局版本。
- `pyenv local`：查看或设置目录特定的版本。
- `pyenv shell`：临时设置当前 shell 的版本。

通过这些命令，你可以方便地管理 `pyenv` 中的 Python 版本。
