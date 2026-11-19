# GB28181 设备模拟器 · Windows 版

**解压即用**：双击 `启动模拟器.bat` 即可，浏览器会自动打开 `http://127.0.0.1:9527`。

## 内容

| 文件                    | 说明                               |
| ----------------------- | ---------------------------------- |
| `GB28181_simulator.exe` | 主程序                             |
| `ffmpeg.exe`            | 内置转码工具，无需另外安装         |
| `启动模拟器.bat`        | 启动入口                           |
| `config.yaml`           | 首次运行自动生成，保存环境与设备组 |

## 使用

1. 双击 `启动模拟器.bat`
2. 页面里选 SIP 服务器（首次需要新建环境）
3. 添加组和通道，给通道选本地视频
4. 点「保存并注册」
5. 去平台点播

## 说明

- 程序优先使用**同目录**的 `ffmpeg.exe`，其次才找系统 PATH
- 控制台端口默认 9527，可在 `config.yaml` 的 `http_port` 修改，改完重启生效
- 设备编号不能与平台已有设备重复，也不要等于平台自己的编号


# GB28181 设备模拟器 · Linux 版

**解压即用**：解压后执行 `./start.sh start`，控制台地址会打印出来。

## 内容

| 文件                | 说明                               |
| ------------------- | ---------------------------------- |
| `GB28181_simulator` | 主程序（amd64）                    |
| `ffmpeg`            | 内置转码工具，无需另外安装         |
| `start.sh`          | 启停脚本                           |
| `config.yaml`       | 首次运行自动生成，保存环境与设备组 |

## 部署

```bash
mkdir -p /data/apps/GB28181_simulator
cd /data/apps/GB28181_simulator
# 把本目录所有文件传上来
chmod +x GB28181_simulator start.sh ffmpeg
./start.sh start
```

输出：

```
已启动，PID=12345
控制台地址: http://192.168.88.51:9527
日志: /data/apps/GB28181_simulator/app.log
```

## 常用命令

```bash
./start.sh status
./start.sh stop
./start.sh restart
tail -f app.log
```

## 说明

- 程序优先使用**同目录**的 `ffmpeg`，其次才找系统 PATH
- 控制台监听 `0.0.0.0`，可从其他机器访问；端口在 `config.yaml` 的 `http_port` 修改
- 视频文件在页面里填**绝对路径**，Linux 没有文件选择对话框
- 内置 ffmpeg 为 x86_64 动态链接版本，适用于 BC-Linux / CentOS 8+ / openEuler 等同系系统；若换到 Ubuntu 等发行版报 glibc 错误，替换成静态版 ffmpeg 即可
