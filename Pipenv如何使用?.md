# Pipenv如何使用？

_Pipenv 是一个 Python 依赖管理工具，结合了 `pip` 和 `virtualenv` 的功能，能够自动管理虚拟环境和项目依赖。以下是 Pipenv 的详细使用指南：_

---

### **1. 安装 Pipenv**
确保已安装 Python 3.6+，然后通过 pip 安装 Pipenv：
```bash
pip install pipenv
```
或（推荐使用用户目录安装避免权限问题）：
```bash
pip install --user pipenv
```

---

### **2. 创建虚拟环境并管理依赖**
#### **初始化项目**
在项目目录下运行：
```bash
pipenv install
```
这会创建虚拟环境（目录默认在 `~/.local/share/virtualenvs/` 或项目目录下的 `.venv`）。

#### **安装包**
- 安装项目依赖（写入 `Pipfile`）：
  ```bash
  pipenv install requests
  ```
- 安装开发依赖（如测试工具）：
  ```bash
  pipenv install pytest --dev
  ```

#### **卸载包**
```bash
pipenv uninstall requests
```

---

### **3. 激活虚拟环境**
```bash
pipenv shell
```
激活后，命令行提示符会显示虚拟环境名称。退出环境输入 `exit`。

#### **直接运行命令（不激活环境）**
```bash
pipenv run python script.py
```

---

### **4. 依赖文件说明**
- **`Pipfile`**：替代 `requirements.txt`，记录依赖和版本。
- **`Pipfile.lock`**：锁定依赖版本，确保环境一致性（需提交到版本控制）。

---

### **5. 其他常用命令**
| 命令 | 说明 |
|------|------|
| `pipenv lock` | 生成/更新 `Pipfile.lock` |
| `pipenv --venv` | 查看虚拟环境路径 |
| `pipenv --rm` | 删除虚拟环境 |
| `pipenv graph` | 查看依赖树 |
| `pipenv install --ignore-pipfile` | 使用 `Pipfile.lock` 安装精确版本 |

---

### **6. 配置镜像源（加速安装）**
在 `Pipfile` 中添加：
```toml
[[source]]
url = "https://pypi.tuna.tsinghua.edu.cn/simple"
verify_ssl = true
name = "pypi"
```

或临时指定：
```bash
pipenv install requests --pypi-mirror https://pypi.tuna.tsinghua.edu.cn/simple
```

---

### **7. 常见问题**
- **找不到命令**：确保 Pipenv 的安装路径在 `PATH` 中（如 `~/.local/bin`）。
- **虚拟环境位置**：通过 `PIPENV_VENV_IN_PROJECT=1` 环境变量可将环境创建在项目目录内。
- **与 `requirements.txt` 转换**：
  - 生成 `requirements.txt`：
    ```bash
    pipenv lock -r > requirements.txt
    ```
  - 从 `requirements.txt` 创建 `Pipfile`：
    ```bash
    pipenv install -r requirements.txt
    ```

---

### **8. 最佳实践**
- 将 `Pipfile` 和 `Pipfile.lock` 提交到 Git。
- 团队中使用 `pipenv sync` 确保依赖一致。
- 避免直接修改 `Pipfile.lock`。

---

通过 Pipenv，你可以更高效地管理 Python 项目的依赖和虚拟环境，避免版本冲突和环境污染。
