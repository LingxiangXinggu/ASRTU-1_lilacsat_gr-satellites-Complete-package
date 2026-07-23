ASRTU-1 便携地面站
====================

这是已经配置好的 GNU Radio / Radioconda、ASRTU-1、Orbitron、SDRSharp 和 DDE 文件夹。
整个目录解压到任意位置后，优先使用根目录的 .cmd 启动文件，不要使用旧电脑上的桌面快捷方式。

推荐启动顺序
------------
1. 双击“Start Orbitron + SDRSharp.cmd”，使用 Orbitron + SDRSharp + DDE 自动多普勒。
2. 使用音频接收时，双击“Start ASRTU-1 Audio.cmd”。电台输出 12 kHz IF，Windows 默认录音设备设置为 USB 音频，采样率 48 kHz。
3. 使用 RTL-SDR 时，双击“Start ASRTU-1 RTL-SDR.cmd”。该流程使用 Plan13 自动多普勒补偿。

ASRTU-1.exe 监听 TCP 127.0.0.1:9985，上传代理使用 ZMQ tcp://127.0.0.1:5555。
上传支路会自动清除 PDU metadata；本地图像解码支路保留原始 PDU。

首次换电脑
----------
- RTL-SDR：以管理员运行 optional_installers\zadig-2.9.exe，为 RTL2832U 的 Bulk-In Interface 0 安装 WinUSB。
- SDRplay：只有使用 SDRplay 硬件时才安装 optional_installers\SDRplay_RSP_API-Windows-2.13.1.exe。
- 音频路由：需要虚拟音频线时安装 optional_installers\VBCABLE_Driver_Pack45.zip 中的驱动。
- Windows 可能拦截旧版 VB6 WiSP DDE；需要时先以管理员运行其目录中的运行库安装程序。

修改呼号和位置
--------------
编辑 asrtu\gnu\config.cfg：proxy_nickname、proxy_long、proxy_lat、proxy_alt 必须保留浮点格式，例如 110.0。
Orbitron 当前站点为 Harbin，经度 126.6095、纬度 45.7297、海拔 110 m；换台址时也请在 Orbitron 的 Location 中修改。
启动文件每次都会根据当前包位置自动修正 Orbitron 和 SDRSharp 的路径。

说明
----
- 本包使用 GNU Radio 3.8.3.1 和 gr-satellites 3.9 兼容环境。ASRTU-1 的 GRC 解码定义已补入，Satellite decoder 按 NORAD 61781 工作。
- 当前机器没有检测到 RTL-SDR，实际射频接收需要插入设备后再验证。
- 不要把包内 radioconda 目录单独挪走；启动文件依赖它与本文件夹的相对位置。
