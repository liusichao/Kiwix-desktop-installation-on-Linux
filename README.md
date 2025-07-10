# 问题二十二、可根据需求加装 CI/CD（如 GitHub Actions 或 Jenkins）自动批量构建。
# libkiwix 使用 Meson 和 Ninja 自动化批量编译详解（基于官方 README）

## 1. 环境准备

### 安装依赖

```bash
sudo apt update
sudo apt install git python3 python3-pip ninja-build pkg-config
sudo apt install zlib1g-dev libcurl4-openssl-dev libzim-dev libmicrohttpd-dev libssl-dev libzip-dev
```
- Meson 推荐使用最新版：  
  ```bash
  sudo pip3 install --upgrade meson
  ```

### 依赖说明
- Meson ≥ 0.45
- Ninja
- pkg-config
- 其他依赖库见上

---

## 2. 获取源码

```bash
git clone https://github.com/kiwix/libkiwix.git
cd libkiwix
```

如需特定版本可查看 tag 并切换：

```bash
git tag                  # 查看所有版本
git checkout v8.2.0      # 示例：切换到 8.2.0 版本
```

---

## 3. 使用 Meson 配置构建目录

推荐 out-of-tree 构建（即不在源码树内编译）：

```bash
meson setup builddir
```
- 可加参数指定 Release 构建：
  ```bash
  meson setup builddir --buildtype=release
  ```
- 如需静态库，可加参数（但一般默认动态库足够）：
  ```bash
  meson setup builddir --default-library=static
  ```

---

## 4. 使用 Ninja 编译

进入构建目录：

```bash
cd builddir
ninja
```
或直接一步编译（在源码根目录下）：

```bash
ninja -C builddir
```

---

## 5. 安装

```bash
sudo ninja install
```
- 默认会安装到 `/usr/local/lib` 和 `/usr/local/include`，可通过 Meson 参数自定义前缀：
  ```bash
  meson setup builddir --prefix=/your/custom/prefix
  ```

---

## 6. 验证

```bash
ls /usr/local/lib | grep kiwix
ls /usr/local/include | grep kiwix
```
或检查 `libkiwix.so`、头文件等是否安装到指定前缀。

---

## 7. 自动化批量构建建议

- 将上述步骤写为 Shell 脚本，适合 CI/CD 或批量部署。
- 可增加参数自动切换分支或版本。
- 如依赖库需定制，也请提前批量编译好。
- **可根据需求加装 CI/CD（如 GitHub Actions 或 Jenkins）自动批量构建：**
  - 针对 GitHub Actions，可新建 `.github/workflows/build.yml`，定义自动化流程。
  - 针对 Jenkins，可编写 Jenkinsfile 或 Freestyle Job 配置，自动拉取、编译、安装。
  - 可参照如下 GitHub Actions 示例：
    ```yaml
    name: Build libkiwix

    on: [push, pull_request]

    jobs:
      build:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v4
        - name: Install dependencies
          run: |
            sudo apt update
            sudo apt install -y python3 python3-pip ninja-build pkg-config zlib1g-dev libcurl4-openssl-dev libzim-dev libmicrohttpd-dev libssl-dev libzip-dev
            sudo pip3 install --upgrade meson
        - name: Build
          run: |
            meson setup builddir
            ninja -C builddir
        - name: Install (optional)
          run: |
            sudo ninja -C builddir install
    ```

---

## 8. 清理构建产物（可选）

```bash
rm -rf builddir
```

---

## 9. 官方参考

- [libkiwix README](https://github.com/kiwix/libkiwix/blob/main/README.md)

---

如遇具体报错，请贴出终端输出以便进一步协助。

---

# 问题二十三、可根据需求加装 CI/CD（如 GitHub Actions 或 Jenkins）自动批量构建。请给出详细的操作步骤
# libkiwix Meson+Ninja 自动化批量构建：CI/CD (以 GitHub Actions/Jenkins 为例)

---

## 1. GitHub Actions 自动化构建配置

### 1.1 新建工作流文件

在 libkiwix 仓库根目录下新建 `.github/workflows/build.yml`：

```yaml
name: Build and Test libkiwix

on:
  push:
    branches: [ main, master ]
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Install dependencies
        run: |
          sudo apt-get update
          sudo apt-get install -y python3 python3-pip ninja-build pkg-config \
            zlib1g-dev libcurl4-openssl-dev libzim-dev libmicrohttpd-dev libssl-dev libzip-dev
          sudo pip3 install --upgrade meson

      - name: Configure (meson)
        run: meson setup builddir --buildtype=release

      - name: Build (ninja)
        run: ninja -C builddir

      - name: Install (optional, test)
        run: sudo ninja -C builddir install

      - name: Test (可选)
        run: |
          cd builddir
          meson test || true
```

**说明：**
- 可根据实际分支调整 `branches`。
- `Install`、`Test` 步骤可按需开启或精简。
- 可加 cache、artifact 上传等增强功能。

---

## 2. Jenkins 自动化构建配置

### 2.1 基础思路

- 新建 Freestyle 或 Pipeline Job
- 拉取源码，安装依赖，meson+ ninja 编译

### 2.2 Pipeline 示例（Jenkinsfile）

在项目根目录新建 `Jenkinsfile`：

```groovy
pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Install Dependencies') {
      steps {
        sh '''
          sudo apt-get update
          sudo apt-get install -y python3 python3-pip ninja-build pkg-config \
            zlib1g-dev libcurl4-openssl-dev libzim-dev libmicrohttpd-dev libssl-dev libzip-dev
          sudo pip3 install --upgrade meson
        '''
      }
    }
    stage('Configure') {
      steps {
        sh 'meson setup builddir --buildtype=release'
      }
    }
    stage('Build') {
      steps {
        sh 'ninja -C builddir'
      }
    }
    stage('Install (optional)') {
      steps {
        sh 'sudo ninja -C builddir install'
      }
    }
    stage('Test (optional)') {
      steps {
        sh 'cd builddir && meson test || true'
      }
    }
  }
}
```

---

## 3. 高级建议

- 可在 CI 配置里加缓存（如 apt/yarn/pip）和 artifacts（如构建产物上传）。
- 可按需并行多平台/多版本编译。
- 可在触发器中加定时、标签、PR 检查等。
- 可自动上传二进制到 Release、包管理等。

---

## 4. 参考链接

- [GitHub Actions 官方文档](https://docs.github.com/en/actions)
- [Jenkins Pipeline 官方文档](https://www.jenkins.io/doc/book/pipeline/)
- [libkiwix 官方 README](https://github.com/kiwix/libkiwix/blob/main/README.md)

---

如有具体平台或报错需求，可贴出详细信息获取进一步帮助。

---

# 问题二十四、可根据需求加装 CI/CD（如 GitHub Actions 或 Jenkins）自动批量构建。请分别给出在GitHub Actions与Jenkins详细的构建步骤和方法
# libkiwix 自动化批量构建：GitHub Actions 与 Jenkins 详细配置步骤

---

## 一、使用 GitHub Actions 自动批量构建

### 步骤 1：新建工作流文件

在 libkiwix 仓库根目录下创建 `.github/workflows/build.yml` 文件。

### 步骤 2：填写工作流内容

```yaml
name: Build libkiwix

on:
  push:
    branches: [ main, master ]
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: 安装依赖
        run: |
          sudo apt-get update
          sudo apt-get install -y python3 python3-pip ninja-build pkg-config \
            zlib1g-dev libcurl4-openssl-dev libzim-dev libmicrohttpd-dev libssl-dev libzip-dev
          sudo pip3 install --upgrade meson

      - name: 配置 (meson)
        run: meson setup builddir --buildtype=release

      - name: 编译 (ninja)
        run: ninja -C builddir

      - name: 安装（可选）
        run: sudo ninja -C builddir install

      - name: 测试（可选）
        run: |
          cd builddir
          meson test || true
```

### 步骤 3：推送代码到 GitHub

- 将 `.github/workflows/build.yml` 提交推送到远程仓库。
- 每次 push 或 PR，GitHub Actions 会自动在 Ubuntu 虚拟机上完成上述编译流程。

---

## 二、使用 Jenkins 自动批量构建

### 步骤 1：准备 Jenkins 环境

- 安装 Jenkins（参考[官方文档](https://www.jenkins.io/doc/book/installing/)）。
- 安装必要插件（推荐：Git、Pipeline）。

### 步骤 2：新建构建任务

- 登录 Jenkins，点击“新建任务”。
- 选择“流水线(Pipeline)”类型，填写名称，创建。

### 步骤 3：配置 Pipeline（流水线）

#### 方法 A：在 Jenkins Web 界面填写 Pipeline 脚本

在 Pipeline 配置中粘贴如下内容：

```groovy
pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Install Dependencies') {
      steps {
        sh '''
          sudo apt-get update
          sudo apt-get install -y python3 python3-pip ninja-build pkg-config \
            zlib1g-dev libcurl4-openssl-dev libzim-dev libmicrohttpd-dev libssl-dev libzip-dev
          sudo pip3 install --upgrade meson
        '''
      }
    }
    stage('Configure') {
      steps {
        sh 'meson setup builddir --buildtype=release'
      }
    }
    stage('Build') {
      steps {
        sh 'ninja -C builddir'
      }
    }
    stage('Install (optional)') {
      steps {
        sh 'sudo ninja -C builddir install'
      }
    }
    stage('Test (optional)') {
      steps {
        sh 'cd builddir && meson test || true'
      }
    }
  }
}
```

#### 方法 B：在项目根目录添加 `Jenkinsfile`

- 将上述脚本保存为 `Jenkinsfile`，提交到仓库。
- 在 Jenkins 新建任务时选择“流水线脚本来自 SCM”（即选用此文件）。

### 步骤 4：保存任务并运行

- 点击“保存”，手动或定时触发构建。
- Jenkins 会自动拉取源码、安装依赖、编译、安装和可选测试。

---

## 三、常见建议与问题解决

- **依赖库需提前准备**：如 libzim、libmicrohttpd 等建议提前批量自动化构建后装入 CI 环境中，或写入依赖安装步骤。
- **缓存优化**：对于依赖不频繁变更的项目，可启用缓存机制减少安装时间。
- **多平台支持**：可用 matrix 策略（GitHub Actions）或 Jenkins 多节点，实现多平台或多架构批量构建。
- **构建产物管理**：可用 artifacts（GitHub Actions）或归档（Jenkins）保存和管理构建好的二进制文件或日志。

---

## 参考资料

- [libkiwix 官方 README](https://github.com/kiwix/libkiwix/blob/main/README.md)
- [GitHub Actions 文档](https://docs.github.com/en/actions)
- [Jenkins Pipeline 文档](https://www.jenkins.io/doc/book/pipeline/)

---

# 问题二十五、可根据需求加装 CI/CD（如 GitHub Actions 或 Jenkins）自动批量构建。请分别给出在GitHub Actions与Jenkins详细的构建步骤和操作方法，以及使用的工具。
# libkiwix 自动批量构建：GitHub Actions 与 Jenkins 详细操作指南

---

## 一、GitHub Actions 自动批量构建

### 1. 工具与前提

- **平台**：GitHub Actions（无需自建服务器，GitHub 官方云端 CI/CD）
- **核心工具**：
  - actions/checkout
  - apt 包管理器（安装依赖）
  - python3-pip、meson、ninja-build、pkg-config
  - 可选：actions/upload-artifact、actions/cache

### 2. 操作步骤

#### 2.1 新建工作流文件

在 libkiwix 仓库根目录下创建 `.github/workflows/build.yml` 文件。

#### 2.2 编辑工作流内容

```yaml
name: Build libkiwix

on:
  push:
    branches: [ main, master ]
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: 安装依赖
        run: |
          sudo apt-get update
          sudo apt-get install -y python3 python3-pip ninja-build pkg-config \
            zlib1g-dev libcurl4-openssl-dev libzim-dev libmicrohttpd-dev libssl-dev libzip-dev
          sudo pip3 install --upgrade meson

      - name: Meson 配置
        run: meson setup builddir --buildtype=release

      - name: Ninja 编译
        run: ninja -C builddir

      - name: 安装（可选）
        run: sudo ninja -C builddir install

      - name: 测试（可选）
        run: |
          cd builddir
          meson test || true

      # 可选：上传二进制产物
      # - name: 上传构建产物
      #   uses: actions/upload-artifact@v4
      #   with:
      #     name: libkiwix-build
      #     path: builddir/
```

#### 2.3 推送并触发

- 提交 `.github/workflows/build.yml` 到仓库。
- 每次 push/PR 会自动触发构建。

---

## 二、Jenkins 自动批量构建

### 1. 工具与前提

- **平台**：Jenkins（需自建或云端 Jenkins 服务）
- **核心工具**：
  - Jenkins（推荐 LTS 版）
  - Git 插件
  - Pipeline 插件
  - 构建节点需有：apt、python3-pip、meson、ninja-build、pkg-config

### 2. 操作步骤

#### 2.1 部署 Jenkins

- 按[官方文档](https://www.jenkins.io/doc/book/installing/)安装 Jenkins 服务及基础插件（Git、Pipeline）。

#### 2.2 新建流水线任务

- 进入 Jenkins → 新建任务 → 输入名称 → 选择“流水线(Pipeline)” → 确定。

#### 2.3 配置 Pipeline 脚本

可在“流水线”配置区直接粘贴脚本，或在仓库根目录新建 `Jenkinsfile` 并配置任务读取。

```groovy
pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }
    stage('Install Dependencies') {
      steps {
        sh '''
          sudo apt-get update
          sudo apt-get install -y python3 python3-pip ninja-build pkg-config \
            zlib1g-dev libcurl4-openssl-dev libzim-dev libmicrohttpd-dev libssl-dev libzip-dev
          sudo pip3 install --upgrade meson
        '''
      }
    }
    stage('Configure') {
      steps {
        sh 'meson setup builddir --buildtype=release'
      }
    }
    stage('Build') {
      steps {
        sh 'ninja -C builddir'
      }
    }
    stage('Install (optional)') {
      steps {
        sh 'sudo ninja -C builddir install'
      }
    }
    stage('Test (optional)') {
      steps {
        sh 'cd builddir && meson test || true'
      }
    }
    stage('Archive Artifacts (optional)') {
      steps {
        archiveArtifacts artifacts: 'builddir/**/*', onlyIfSuccessful: true
      }
    }
  }
}
```

#### 2.4 保存并运行

- 保存任务配置。
- 手动或定时触发构建，Jenkins 会自动完成拉取、依赖安装、编译、测试、归档。

---

## 三、补充建议

- **依赖管理**：建议所有依赖自动安装在流水线中，确保环境一致性。
- **缓存加速**：可用 actions/cache 或 Jenkins Cache 插件缓存依赖。
- **多平台并行**：GitHub Actions 支持 matrix 策略，Jenkins 可用多节点并发。
- **归档产物**：通过上传 artifact 或 archiveArtifacts 保留二进制和日志。
- **通知集成**：可集成邮件、Slack、微信等通知插件。

---

## 参考资料

- [libkiwix README](https://github.com/kiwix/libkiwix/blob/main/README.md)
- [GitHub Actions 官方文档](https://docs.github.com/en/actions)
- [Jenkins 官方文档](https://www.jenkins.io/doc/)

---

