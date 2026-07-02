# ADB

用于回答 Quest ADB 安装、连接、文件传输、日志、截图、录屏、启动或关闭应用等问题。

## Permission Rule

ADB 会直接操作用户设备。给命令前先说明用途、影响和恢复方式。需要实际执行命令时，必须先询问：

- 用户自己复制命令执行；或
- 用户明确授权 agent 代为执行。

未获得明确许可前，不要对连接的 Quest 执行 ADB 命令。

## Official Tools

优先使用官方来源：

- Android SDK Platform Tools：用于 `adb`。
- Meta Quest Developer Hub：用于设备管理、日志和开发调试。
- Meta 官方开发者文档：用于确认当前开发者模式、USB 调试和设备要求。

涉及工具版本或页面入口时，先核实当前官方文档。

## Connect And Verify

```powershell
adb kill-server
adb start-server
adb devices
```

如果显示 `unauthorized`，戴上头显确认 USB debugging 弹窗。

查看设备信息：

```powershell
adb shell getprop ro.product.model
adb shell getprop ro.build.version.release
adb shell df -h
```

## Install Authorized APK

只用于本人开发、公司测试、开源或已获得授权的 APK。

```powershell
adb install .\app.apk
adb install -r .\app.apk
adb uninstall com.example.app
```

常见报错：

- `INSTALL_FAILED_VERSION_DOWNGRADE`：新包版本号低于已安装版本。
- `INSTALL_FAILED_INSUFFICIENT_STORAGE`：空间不足。
- `device unauthorized`：头显没有确认 USB debugging。

## File Transfer

推送文件到 Quest：

```powershell
adb push .\movie.mp4 /sdcard/Movies/
adb push .\Pictures\image.jpg /sdcard/Pictures/
adb shell mkdir -p /sdcard/Download/MyFiles
```

从 Quest 导出文件：

```powershell
adb pull /sdcard/Oculus/Screenshots .\Quest-Screenshots
adb pull /sdcard/Oculus/VideoShots .\Quest-Recordings
adb pull /sdcard/Download .\Quest-Download
```

查看目录：

```powershell
adb shell ls /sdcard/
adb shell ls /sdcard/Download/
```

## Logs, Screenshot, And Recording

导出日志前提醒用户：日志可能包含设备名、路径、应用包名和局域网信息。

```powershell
adb logcat -d > quest-log.txt
adb exec-out screencap -p > quest-screen.png
adb shell screenrecord /sdcard/Download/quest-record.mp4
adb pull /sdcard/Download/quest-record.mp4 .\quest-record.mp4
```

停止录屏：按 `Ctrl+C`。

## Start Or Stop Apps

查找包名：

```powershell
adb shell pm list packages
adb shell pm list packages | findstr example
```

启动应用：

```powershell
adb shell monkey -p com.example.app 1
```

强制停止应用：

```powershell
adb shell am force-stop com.example.app
```

不要强制停止系统 UI、账号服务、追踪、控制器、商店或其他关键系统组件。

## Wi-Fi Limited Status Diagnostic

这只用于处理 Android 联网检测误判，不会修复真实断网、路由器故障或服务侧问题。

查看当前检测配置：

```powershell
adb shell settings get global captive_portal_mode
adb shell settings get global captive_portal_https_url
adb shell settings get global captive_portal_http_url
```

恢复系统默认检测：

```powershell
adb shell settings delete global captive_portal_mode
adb shell settings delete global captive_portal_https_url
adb shell settings delete global captive_portal_http_url
adb reboot
```

如果仍显示受限，继续排查 Wi-Fi 密码、路由器、DNS、系统时间、AP 隔离和 Meta 服务状态。

