# 如何安装配置gitbook，请给出最为详尽的安装配置步骤和方法并一一列出各个选项并说明它们各自的用途。

## 以下是 **GitBook 最详尽的安装配置指南**，涵盖从环境准备到项目搭建的全流程，并详细说明每个步骤的用途及注意事项：

### 一、环境准备
#### 1. 安装 Node.js（核心依赖）
- **用途**：GitBook 基于 Node.js 运行，需提前安装。
- **步骤**：
  - **下载 LTS 版本**：访问 [Node.js 官网](https://nodejs.org/)，选择 **LTS（长期支持版）**（如 18.x 或 16.x），避免使用最新版（可能存在兼容性问题）。
  - **安装**：双击下载的 `.msi`（Windows）或 `.pkg`（Mac）文件，按向导完成安装。
  - **验证**：
    ```bash
    node -v  # 查看 Node.js 版本
    npm -v   # 查看 npm 版本（Node.js 自带）
    ```

#### 2. 配置 npm 镜像（可选，加速依赖下载）
- **用途**：国内用户建议切换为淘宝镜像，提升下载速度。
- **命令**：
  ```bash
  npm config set registry https://registry.npmmirror.com
  npm config get registry  # 验证是否配置成功
  ```

### 二、安装 GitBook CLI
#### 1. 全局安装 GitBook 命令行工具
- **用途**：`gitbook-cli` 是管理 GitBook 版本和生成书籍的核心工具。
- **命令**：
  ```bash
  npm install -g gitbook-cli
  ```
- **验证安装**：
  ```bash
  gitbook -V  # 查看 GitBook CLI 版本
  ```
  - **首次运行**：会自动下载 GitBook 默认版本（如 3.2.3）。

#### 2. 解决常见安装问题
- **问题 1**：`cb.apply is not a function` 错误  
  - **原因**：Node.js 版本过高（如 20.x）。  
  - **解决方案**：  
    - 降级 Node.js 至 18.x 或 16.x（推荐使用 [nvm](https://github.com/nvm-sh/nvm) 管理多版本）。  
    - 或手动修改文件：  
      找到报错路径（如 `/usr/local/lib/node_modules/gitbook-cli/node_modules/npm/node_modules/graceful-fs/polyfills.js`），注释掉以下代码：
      ```javascript
      // fs.stat = statFix(fs.stat);
      // fs.fstat = statFix(fs.fstat);
      // fs.lstat = statFix(fs.lstat);
      ```

- **问题 2**：权限不足（Mac/Linux）  
  - **解决方案**：在命令前加 `sudo`（不推荐长期使用）或修复 npm 权限：
    ```bash
    sudo chown -R $(whoami) ~/.npm
    ```

### 三、创建并初始化 GitBook 项目
#### 1. 创建项目目录
- **命令**：
  ```bash
  mkdir my-gitbook && cd my-gitbook  # 创建并进入目录
  ```

#### 2. 初始化项目
- **命令**：
  ```bash
  gitbook init
  ```
- **生成文件**：
  - `README.md`：书籍的介绍页（默认内容为 `# Introduction`）。
  - `SUMMARY.md`：目录结构文件（需手动编辑以添加章节）。

#### 3. 编辑目录结构（`SUMMARY.md`）
- **示例**：
  ```markdown
  # Summary
  * [前言](README.md)
  * [第一章：GitBook 基础](chapter1/README.md)
    * [1.1 安装与配置](chapter1/section1.md)
    * [1.2 基本命令](chapter1/section2.md)
  * [第二章：进阶用法](chapter2/README.md)
  ```
- **规则**：
  - 使用 Markdown 列表语法定义章节层级。
  - 路径需指向实际存在的 `.md` 文件（否则生成时会报错）。

#### 4. 创建章节文件
- **手动创建**：根据 `SUMMARY.md` 中的路径，新建对应的 `.md` 文件（如 `chapter1/section1.md`）。

### 四、配置书籍信息（`book.json`）
#### 1. 创建配置文件
- **命令**：
  ```bash
  touch book.json
  ```
- **示例配置**：
  ```json
  {
    "title": "我的第一本 GitBook",
    "author": "你的名字",
    "description": "GitBook 入门教程",
    "language": "zh-hans",  // 中文简体
    "gitbook": "3.2.3",     // 指定 GitBook 版本
    "structure": {
      "readme": "README.md", // 介绍页
      "summary": "SUMMARY.md" // 目录页
    },
    "plugins": ["search", "sharing", "fontsettings"], // 启用插件
    "pluginsConfig": {
      "sharing": {
        "facebook": false,
        "twitter": false
      }
    }
  }
  ```
- **关键选项**：
  - `title`/`author`/`description`：书籍元信息。
  - `language`：支持 `zh-hans`（简体）、`en`（英文）等。
  - `plugins`：启用官方插件（如搜索、分享按钮）。
  - `pluginsConfig`：自定义插件行为（如隐藏社交分享按钮）。

### 五、预览与生成书籍
#### 1. 本地预览
- **命令**：
  ```bash
  gitbook serve
  ```
- **效果**：
  - 自动打开浏览器访问 `http://localhost:4000`。
  - 实时监听文件变化并刷新页面（修改 `.md` 文件后无需重启服务）。

#### 2. 生成静态网站
- **命令**：
  ```bash
  gitbook build
  ```
- **输出目录**：`_book/`（包含 HTML、CSS、JS 等文件，可直接部署到服务器）。

#### 3. 生成电子书格式（需安装 Calibre）
- **安装 Calibre**：
  - 下载地址：[https://calibre-ebook.com/download](https://calibre-ebook.com/download)
- **生成 PDF/EPUB/MOBI**：
  ```bash
  gitbook pdf ./ mybook.pdf
  gitbook epub ./ mybook.epub
  gitbook mobi ./ mybook.mobi
  ```

### 六、高级用法
#### 1. 使用自定义主题
- **步骤**：
  1. 克隆主题仓库（如 `gitbook-theme-yue`）：
     ```bash
     git clone https://github.com/your-repo/theme.git _theme
     ```
  2. 在 `book.json` 中指定主题：
     ```json
     {
       "styles": {
         "website": "_theme/styles/website.css"
       }
     }
     ```

#### 2. 部署到 GitHub Pages
- **步骤**：
  1. 生成静态网站：
     ```bash
     gitbook build
     ```
  2. 将 `_book/` 目录内容推送到 GitHub 仓库的 `gh-pages` 分支。

### 七、常见问题排查
1. **端口冲突**：  
   - 默认端口 `4000` 被占用时，可通过 `--port` 指定新端口：
     ```bash
     gitbook serve --port 8080
     ```

2. **插件安装失败**：  
   - 确保网络正常，或尝试手动安装插件：
     ```bash
     gitbook install ./node_modules/gitbook-plugin-<plugin-name>
     ```

3. **Markdown 语法错误**：  
   - 使用 [Markdown 校验工具](https://dillinger.io/) 检查文件格式。
