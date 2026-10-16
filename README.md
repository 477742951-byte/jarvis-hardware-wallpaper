# J.A.R.V.I.S. 实时硬件监控壁纸

为 Wallpaper Engine 制作的网页壁纸：JARVIS 圆环、神经能量束、硬件数据轮盘与实时监控面板。

## 下载与首次使用

**首次使用需要安装一次配套采集器，之后登录自动运行。仅订阅壁纸不会自动安装程序。**

1. 在 Wallpaper Engine 中订阅并应用本壁纸（工坊发布链接将在完成后补充）。
2. [下载安装器 Companion-Setup.exe](https://github.com/477742951-byte/jarvis-hardware-wallpaper/releases/latest/download/Companion-Setup.exe)。已包含 Python、依赖和传感器组件，不需要自行安装 Python。
3. 运行安装器，选择安装目录，保留“登录后自动采集”和“缺少 PawnIO 时安装驱动”选项，按 Windows 提示授权。
4. 等待几秒，壁纸会自动显示你自己电脑的数据；以后登录后自动连接。

需要手动解压安装时可下载 [Companion-Offline.zip](https://github.com/477742951-byte/jarvis-hardware-wallpaper/releases/latest/download/Companion-Offline.zip)，在解压目录运行：

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File .\scripts\configure.ps1 -InstallPawnIO -EnableStartup -StartNow
```

## 实时数据

- 本机 CPU 利用率、线程、进程占用和内存。
- GPU 利用率、温度、功耗和显存（依硬件支持）。NVIDIA 优先 NVML，其他受支持设备使用 LibreHardwareMonitor。
- 网卡型号及收发速率。
- 实际物理磁盘型号、盘符、读写速率；当前界面展开两块磁盘。
- CPU/GPU 各自根据真实温度逐渐变色并显示高温警告，高负载增强能量活动；阈值可在壁纸设置中调整。

**温度与功耗读取取决于硬件、驱动及权限。不支持的项目显示 N/A，不使用虚构读数。** 跨厂商路径已有测试，实机验证以开发机器为限，不能保证所有设备都开放全部传感器。

## 显示与性能

网页按实际屏幕分辨率绘制，支持 16:10、21:9 等比例；已实测 3440×1440。硬件采样约 250 ms，传感器约 500 ms，进程明细约 2 秒。数据解析使用独立 Worker，动画使用约 300 ms 缓冲。

## 本地运行与维护

数据只在本机采集，不上传云端。后台仅监听 127.0.0.1:18766，网页通道核验 Wallpaper Engine 原生进程，REST 诊断接口使用每台安装独立生成的口令。

开始菜单中的 Start Companion / Stop Companion 可启动或停止采集。卸载使用 Windows“已安装的应用”；会清理自己的后台与启动任务，不移除其他软件可能共用的 PawnIO。

安装目录内的 `runtime` 含私有配置及本机硬件信息，请勿公开上传。配套安装器暂未代码签名；内置 Python 与 PawnIO 保留其官方签名。可用 [SHA256SUMS.txt](https://github.com/477742951-byte/jarvis-hardware-wallpaper/releases/latest/download/SHA256SUMS.txt) 校验下载文件。

## 文件与第三方组件

[最新发布版本](https://github.com/477742951-byte/jarvis-hardware-wallpaper/releases/latest) 同时提供网页项目、离线安装包、源文件与校验清单。

第三方许可保留在安装包的 `licenses` 目录；LibreHardwareMonitor 0.9.6、PawnIO 2.2.0、PawnIO.Modules 0.1.6 对应源码也随离线组件提供。第三方组件各自的许可证保持有效。
