# webvideo-downloader

![](https://img.shields.io/badge/platform-win%20%7C%20linux%20%7C%20osx-brightgreen) ![](https://img.shields.io/badge/python-%3E=%203.5.0-orange)

🚀 视频下载器，用于下载网站中可以在线播放的视频。

---

## 目录

- [功能介绍](#功能介绍)
- [快速开始](#快速开始)
  - [安装](#安装)
  - [运行](#运行)
- [工作原理](#工作原理)
- [更新日志](#更新日志)

## 功能介绍

#### 主要支持网站

| 站点                | URL                                                    | 普通画质 | VIP专属 |
| ------------------- | ------------------------------------------------------ | -------- | ------- |
| 哔哩哔哩（单P/多P） | [https://www.bilibili.com/](https://www.bilibili.com/) | ✓        | ✓       |
| 爱奇艺              | [https://www.iqiyi.com/](https://www.iqiyi.com/)       | ✓        | ✓       |
| 腾讯视频            | [https://v.qq.com/](https://v.qq.com/)                 | ✓        | ✓       |
| 芒果TV              | [https://www.mgtv.com/](https://www.mgtv.com/)         | ✓        | ✓       |
| WeTV                | [https://wetv.vip/](https://wetv.vip/)                 | ✓        | ✓       |
| 爱奇艺国际站        | [https://www.iq.com/](https://www.iq.com/)             | ✓        | ✓       |

此外，备用的 [CommonHlsDownloader](https://github.com/jaysonlong/webvideo-downloader/raw/master/violentmonkey/CommonHlsDownloader.user.js) 脚本支持绝大部分基于 HLS 流式视频的网站，如 [LPL官网](https://lpl.qq.com/) 等。

#### 特性

- 跨平台（Windows/Linux/Mac）
- 多线程下载（单文件分段/多文件并行）
- 字幕下载和集成（集成字幕的视频需使用支持字幕的播放器播放，如 `PotPlayer`，`VLC Player` 等）

#### 关于 VIP

本项目支持**1080p蓝光画质、VIP专享、VIP点播、付费视频**的下载，前提是你是VIP/用了券/付了费。

> **What you can watch determined what you can download.**
>
> 你只能下载你或你的账号可以在线观看的视频，本项目没有VIP破解功能。


## 快速开始

### 安装

##### *安装依赖程序*

本项目基于[Python](https://www.python.org/)、[FFmpeg](https://ffmpeg.org/) 和浏览器扩展 [Violentmonkey](https://violentmonkey.github.io/)/[Tampermonkey](https://www.tampermonkey.net/) 开发：

- [Python](https://www.python.org/) (3.5 或以上)
- [FFmpeg](https://ffmpeg.org/) (Windows 系统无需安装，已内置到仓库中)
- [Violentmonkey](https://violentmonkey.github.io/) /  [Tampermonkey](https://www.tampermonkey.net/) (二选一)

##### *获取项目*

直接下载压缩包，或使用 git clone：

```
git clone https://github.com/jaysonlong/webvideo-downloader.git
```

##### *安装项目*

浏览器安装以下基于 Violentmonkey/Tampermonkey 的脚本。直接点击以下链接即可安装：

- [WebVideoDownloader 脚本](https://github.com/jaysonlong/webvideo-downloader/raw/master/violentmonkey/WebVideoDownloader.user.js)（主脚本，支持6个主流网站视频下载）

- [CommonHlsDownloader 脚本](https://github.com/jaysonlong/webvideo-downloader/raw/master/violentmonkey/CommonHlsDownloader.user.js)（通用 HLS 下载脚本，按需安装，作用于除以上6个主流网站以外的使用 HLS 的网站）

安装 python 依赖包：

```
cd webvideo-downloader/downloader
pip install -r requirements.txt
```

（按需安装）浏览器安装广告拦截器：
- [AdGuard 广告拦截器](https://adguard.com/)

> 对于某些网站，视频存在广告时，浏览器插件脚本会延迟到广告即将结束时才能提取到视频链接，安装拦截器可不用等待广告播放完毕

### 运行

> 本项目分为两部分，**Violentmonkey** 目录下的 javascript 脚本用于在浏览器中提取视频链接，**Downloader** 目录下的 python 脚本用于下载、合并视频。

首先执行 python 脚本：

```
python daemon.py
```

然后访问视频网站并点击某个视频，网页会自动弹出下载按钮，点击按钮即可下载。

示例链接：https://www.bilibili.com/video/BV1c741157Wb

![bilibili](img/bilibili.gif)

下载进度可在 python 脚本的命令窗口查看：

```
$ python daemon.py
Listening on port 18888 for clients...

Receive: {
    "fileName": "看小黄书会被处罚吗",
    "linksurl": "http://xxx",
    "type": "link"
}

Handle: "看小黄书会被处罚吗"

匹配到1段音频，1段视频，开始下载
-- dispatcher/downloadDash
正在下载 E:\Workspace\Github\webvideo-downloader\temp\看小黄书会被处罚吗.audio.m4s
分8段, 并行8线程下载
进度: [########################################] 100%    0.9/0.9MB  450KB/s 0s
正在下载 E:\Workspace\Github\webvideo-downloader\temp\看小黄书会被处罚吗.video.m4s
分8段, 并行8线程下载
进度: [########################################] 100%  11.2/11.2MB  5.2MB/s 2s
正在合并视频
Finish.
```

> 下载目录默认为项目根目录下的 videos 文件夹，可在 downloader/config.py 中配置。

python 脚本可选命令行参数：

```
$ python daemon.py -h
usage: daemon.py [-h] [-t:h N] [-t:f N] [-f N] [-p PORT] [-c] [-s] [-d] [-i]

optional arguments:
  -h, --help     show this help message and exit
  -t:h N         the thread count of hls download, default 8
  -t:f N         the thread count of fragments download, default 8
  -f N           the fragments count of each file, default 0 using the thread count
  -p PORT        the port that the backend server listens on, default 18888
  -c, --correct  correct the timestamp of hls video, merge fragments using binnary mode
  -s             if set, will save the temp files
  -d             debug mode, log more info and save the temp files (ignore -s)
  -i             interactive mode, get url and file name from the command line
```
```

$ python daemon.py -h
用法：daemon.py [-h] [-t:h N] [-t:f N] [-f N] [-p PORT] [-c] [-s] [-d] [-i]

可选参数：
  -h, --help     显示此帮助信息并退出
  -t:h N         HLS下载的线程数，默认8
  -t:f N         片段下载的线程数，默认8
  -f N           每个文件的片段数量，默认为0（使用线程数）
  -p PORT        后台服务器监听的端口，默认18888
  -c, --correct  纠正HLS视频的时间戳，使用二进制模式合并片段
  -s             启用时将保存临时文件
  -d             调试模式，记录更多信息并保存临时文件（忽略-s参数）
  -i             交互模式，从命令行获取URL和文件名
```

注：参数格式保持英文原样（如-t:h、-p等），描述部分已翻译为中文。参数默认值保留数字格式，关键术语如"binary mode"译为"二进制模式"，"fragments"译为"片段"，"thread count"译为"线程数"。

---

以下是针对该Python脚本的参数解析和使用指南，帮助您更好地理解和使用该工具：

---

### **核心功能**
这是一个HLS视频下载工具，支持多线程下载、时间戳校正、调试模式等功能，适用于需要高效下载和合并HLS视频流的场景。

---

### **参数详解**

#### **基础控制**
1. **`-h, --help`**  
   - 显示帮助信息，快速查看参数说明。

2. **`-t:h N`**  
   - 设置HLS下载的线程数（默认8）。  
   - *示例*：`-t:h 16` 加速HLS索引文件下载。

3. **`-t:f N`**  
   - 设置分片下载的线程数（默认8）。  
   - *场景*：高带宽环境下可设为`-t:f 32`提升分片下载速度。

4. **`-f N`**  
   - 每个文件的分片数量（默认0，自动匹配线程数）。  
   - *注意*：若设为`-f 10`，即使线程数更高，每个文件也仅拆分为10个分片。

---

#### **服务器配置**
5. **`-p PORT`**  
   - 指定后端服务端口（默认18888）。  
   - *用途*：避免端口冲突时使用，如`-p 20000`。

---

#### **调试与开发**
6. **`-c, --correct`**  
   - 校正HLS视频时间戳，合并时采用二进制模式。  
   - *适用场景*：解决视频时间戳错乱导致的播放问题。

7. **`-s`**  
   - 保留临时文件（如未合并的分片）。  
   - *调试技巧*：结合`-s`和`-d`可分析下载过程。

8. **`-d`**  
   - 调试模式（记录详细日志，强制保留临时文件）。  
   - *日志路径*：通常在当前目录生成`debug.log`。

9. **`-i`**  
   - 交互模式，手动输入URL和文件名。  
   - *示例交互流程*：  
     ```bash
     $ python daemon.py -i
     Enter HLS URL: https://example.com/video.m3u8
     Enter output filename: my_video.mp4
     ```
---

### **使用示例**
1. **基础下载**  
   ```bash
   python daemon.py -t:h 16 -t:f 32 -f 20 https://example.com/video.m3u8
   ```
   - 使用16线程下载HLS索引，32线程下载分片，每个文件拆分20个分片。

2. **调试时间戳问题**  
   ```bash
   python daemon.py -c -d -i
   ```
   - 交互式输入URL，启用时间戳校正和调试模式，保留所有临时文件。

3. **自定义端口和临时文件保存**  
   ```bash
   python daemon.py -p 20000 -s https://example.com/video.m3u8
   ```
   - 服务运行在20000端口，下载完成后保留临时分片。

---

### **常见问题**
1. **下载速度未提升**  
   - 检查线程数是否合理（过高可能导致服务器限速）。
   - 尝试增大`-f`值以增加分片并行度。

2. **合并后视频异常**  
   - 使用`-c`参数校正时间戳。
   - 检查HLS源是否完整（如`.m3u8`文件是否包含所有分片）。

3. **端口冲突**  
   - 修改`-p`参数（如`-p 25000`）或终止占用端口的进程。

---

### **注意事项**
- **资源管理**：高线程数（如`-t:h 64`）可能导致内存或CPU占用过高。
- **临时文件**：默认自动清理，调试时需显式启用`-s`或`-d`。
- **二进制合并**：`-c`参数可能影响视频元数据，建议测试后用于生产环境。

希望这份指南能帮助您高效使用该工具！如有其他问题，可补充具体场景进一步分析。

---

## 工作原理

**浏览器播放视频原理**

用户登录生成session ——> 发送获取视频资源的HTTP请求 ——> 服务器基于session认证用户身份 ——> 认证通过后返回视频资源描述文件（如经典的m3u8文件，其中包含视频的所有分片的下载地址） ——> 浏览器解析描述文件，依次下载每个视频分片，并组装播放

**本项目工作原理**

1、暴力猴脚本：作用于浏览器，通过hook浏览器的HTTP请求（主要为ajax hook和jsonp hook），拦截服务器返回的视频资源描述文件，再将视频资源描述文件通过HTTP请求发送给下载器。

2、下载器：在本机启动一个Web服务器，接收暴力猴脚本发送过来的视频资源描述文件，并解析资源描述文件依次下载所有视频分片（模仿浏览器行为），最终合成单个视频。

## 更新日志

### [v2.0] - 2020-11-09

#### 新增

- 支持腾讯视频长分段下载（由用户上传的视频）
- 支持爱奇艺国际站 VIP 下载、WeTV 无字幕下载
- 增加 debug 模式

#### 变更

- 合并守护模式和交互模式为一个 python 脚本
- 在爱奇艺国际站（iq.com）中禁用 WebAssembly 扩展，防止字幕加密

### [v1.6] - 2020-09-12

#### 新增

- 支持爱奇艺国际站视频下载
- 支持多个字幕文件集成到视频中

### [v1.5] - 2020-09-01

#### 新增

- 支持 WeTV，愛奇藝台灣站视频下载
- 支持部分网站字幕文件集成到视频中
- 下载文件完整性检查

#### 变更

- MP4 文件 moov box 前置，便于网络传输

### [v1.4] - 2020-06-30

#### 变更

- 守护模式运行时端口复用，其监听模式同时支持 HTTP Server 和 WebSocket
- 暴力猴脚本可自定义远程调用模式（HTTP 或 WebSocket）

### [v1.3] - 2020-06-27

#### 变更

- 暴力猴脚本重构 & 界面重写

### [v1.2] - 2020-06-18

#### 新增

- 支持爱奇艺 MPD 格式文件解析
- 支持 MSE 视频流通过 WebSocket导出（实验性）
- 新增两个暴力猴脚本：通用 hls 下载脚本和 MSE 视频流导出脚本（实验性）
- 命令行参数支持

#### 变更

- 守护模式运行时的监听模式由 HTTP Server 更改为 WebSocket 
- 哔哩哔哩多P下载脚本合并到通用下载脚本中

### [v1.1] - 2020-05-29

#### 新增

- 支持基于 HTTP Server 以守护模式运行，浏览器点击链接直接调用后台下载

#### 变更

- 合并4个网站脚本为单个，便于安装和管理

### [v1.0] - 2020-05-26

#### 新增

- 支持哔哩哔哩、爱奇艺、腾讯视频、芒果TV视频下载（手动复制链接粘贴）
  
[v2.0]: https://github.com/jaysonlong/webvideo-downloader/compare/v1.6...v2.0
[v1.6]: https://github.com/jaysonlong/webvideo-downloader/compare/v1.5...v1.6
[v1.5]: https://github.com/jaysonlong/webvideo-downloader/compare/v1.4...v1.5
[v1.4]: https://github.com/jaysonlong/webvideo-downloader/compare/v1.3...v1.4
[v1.3]: https://github.com/jaysonlong/webvideo-downloader/compare/v1.2...v1.3
[v1.2]: https://github.com/jaysonlong/webvideo-downloader/compare/v1.1...v1.2
[v1.1]: https://github.com/jaysonlong/webvideo-downloader/compare/v1.0...v1.1
[v1.0]: https://github.com/jaysonlong/webvideo-downloader/releases/tag/v1.0
