# DeltaForce Mobile

[![Stars](https://img.shields.io/github/stars/ace-trump-tech/deltaforce-mobile?style=social)](https://github.com/ace-trump-tech/deltaforce-mobile/stargazers) [![Forks](https://img.shields.io/github/forks/ace-trump-tech/deltaforce-mobile?style=social)](https://github.com/ace-trump-tech/deltaforce-mobile/network/members) [![Python](https://img.shields.io/badge/Python-3.8%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)

DeltaForce-OBS-Locker 的 Mobile 端下载工具与演示素材独立仓库。仓库本身不包含 APK，`download_apk.py` 负责从你指定的 Hugging Face 仓库下载文件。

> 仅用于下载器、网络可靠性和移动端交互演示学习。安装第三方 APK 前请审查来源、签名和校验和，不要在主力设备上授予未知应用无障碍或悬浮窗权限。

## 项目关系

- 主项目：[DeltaForce-OBS-Locker](https://github.com/ace-trump-tech/DeltaForce-OBS-Locker)
- PC 端：[deltaforce-pc](https://github.com/ace-trump-tech/deltaforce-pc)
- 相关模型项目：[z637826/yolo-omni](https://github.com/z637826/yolo-omni)

## 快速开始

### 1. 获取代码

```bash
git clone https://github.com/ace-trump-tech/deltaforce-mobile.git
cd deltaforce-mobile
```

### 2. 安装依赖

```bash
python3 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install --upgrade pip
pip install -r requirements.txt
```

### 3. 下载文件

脚本要求显式指定 Hugging Face 仓库和文件路径：

```bash
python download_apk.py \
  --repo-id <owner>/<repo> \
  --filename <path/in/repository/Locker_Android.apk> \
  --local-path Locker_Android.apk \
  --threads 1
```

私有仓库可使用环境变量，避免把 token 写进 shell 历史：

```bash
export HF_TOKEN=hf_xxx
python download_apk.py --repo-id <owner>/<repo> --filename <path/to/file.apk>
```

大文件可使用 `--threads 4`；断点续传使用 `--resume`。下载后建议通过发布者提供的 SHA-256 校验和验证文件，再决定是否传输到手机。

## 文件说明

| 文件 | 用途 |
| --- | --- |
| `download_apk.py` | Hugging Face 文件下载器，支持重试、断点、分片和可选 MD5 校验 |
| `requirements.txt` | Python 运行依赖 |
| `demo.png` | 操作流程示意图 |
| `demo_video.gif` | 在线预览动画 |
| `demo_video.mp4` | 本地演示视频 |
| `Protective_suit.jpg` | 示例图片 |

## 下载器参数

```text
--repo-id       Hugging Face 仓库，如 user/repo
--filename      仓库内文件路径
--local-path    本地保存路径
--resume        从已有文件继续下载
--threads       大文件分片线程数
--max-retries   失败重试次数
--md5           可选 MD5 校验值
--token         私有仓库访问令牌（更推荐 HF_TOKEN）
```

运行 `python download_apk.py --help` 查看完整参数。

## 常见问题

**`ModuleNotFoundError: requests`**

确认虚拟环境已激活，并执行 `pip install -r requirements.txt`。

**README 里的 `python download_apk.py` 为什么不够？**

当前脚本不会内置 APK 地址，必须通过 `--repo-id` 和 `--filename` 指定下载源。这是为了避免把未经验证的 APK 地址硬编码在仓库中。

**下载后无法安装？**

先检查文件大小和校验和，再确认 Android 版本、ABI 和签名要求。不要通过关闭系统安全设置来强行安装。

## 许可证与责任

代码和演示素材的许可证与来源请以各自文件和上游项目声明为准。第三方 APK 不由本仓库发布或背书。
