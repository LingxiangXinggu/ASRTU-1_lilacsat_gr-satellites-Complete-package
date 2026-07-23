# 重要：首次运行前必须配置

# 重要：请下载release中的文件，以获取完整应用程序以及readme使用文档。

# 重要：请下载VB-CABLE，https://vb-audio.com/Cable/ 以用来连接SDRSharp到解码软件的音频。

========================

本公开发布版已删除呼号和站点位置。解压后请先完成以下三项，否则上传位置、多普勒补偿和过境计算不正确：

1. 双击“00 Configure Callsign and Upload Location.cmd”。
   在 config.cfg 中填写 proxy_nickname、proxy_long、proxy_lat、proxy_alt。
   经纬度和海拔必须是浮点数，例如 120.0000、30.0000、100.0，不能删除等号后的数值。

2. 双击“01 Configure RTL-SDR Plan13 Location.cmd”。
   在 GNU Radio Companion 中双击 Plan13 CC，填写 Longitude、Latitude、Height，然后保存流程图。

3. 双击“02 Configure Orbitron Location.cmd”。
   在 Orbitron 的 Location 设置中填写接收站名称、经纬度和海拔并保存。

4. 非常重要：打开SDRSharp后，在左侧功能模块内的“基带录制”、“音频录制”中分别修改想要保存的路径，否则软件将会报错并崩溃。

ASRTU-1 便携地面站
====================

这是已经配置好的 GNU Radio / Radioconda、ASRTU-1、Orbitron、SDRSharp 和 DDE 运行目录。
整个目录可解压到任意位置。请使用根目录的 .cmd 文件启动，不要使用旧电脑上的桌面快捷方式。

推荐启动顺序
------------
1. 双击“Start Orbitron + SDRSharp.cmd”，使用 Orbitron + SDRSharp + DDE 自动多普勒。
2. 使用音频接收时，双击“Start ASRTU-1 Audio.cmd”。电台输出 12 kHz IF，Windows 默认录音设备设为 USB 音频，采样率 48 kHz。
3. 使用 RTL-SDR 时，双击“Start ASRTU-1 RTL-SDR.cmd”。该流程使用 Plan13 自动多普勒补偿。

ASRTU-1.exe 监听 TCP 127.0.0.1:9985，上传代理使用 ZMQ tcp://127.0.0.1:5555。
上传支路会自动清除 PDU metadata；本地图像解码支路保留原始 PDU。

首次换电脑
----------
- RTL-SDR：以管理员身份运行 optional_installers\zadig-2.9.exe，为 RTL2832U 的 Bulk-In Interface 0 安装 WinUSB。
- SDRplay：只有使用 SDRplay 硬件时才安装 optional_installers\SDRplay_RSP_API-Windows-2.13.1.exe。
- 音频路由：需要虚拟音频线时安装 optional_installers\VBCABLE_Driver_Pack45.zip 中的驱动。
- Windows 可能拦截旧版 VB6 WiSP DDE；需要时先安装其目录中的运行库。

说明
----
- GNU Radio 版本为 3.8.3.1，gr-satellites 使用 GNU Radio 3.8 兼容环境。
- ASRTU-1 GRC 定义已补入，Satellite decoder 按 NORAD 61781 工作。
- 启动脚本使用相对路径，并会自动修正 Orbitron 和 SDRSharp 的当前解压路径。
- 不要单独移动 radioconda 或其他子目录。
- 打包电脑未检测到 RTL-SDR，实际射频接收仍需接入硬件验证。
