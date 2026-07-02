# Quest ADB 实用指南

## 适用场景

用于回答 Quest 用户关于安装 ADB、连接电脑、安装合法 APK、传输文件、导出截图/录屏、收集日志、查询包名、卸载用户应用等问题。

先确认用户目标是合法开发、调试、安装自有/开源/授权 APK，还是传输个人文件。不要帮助安装盗版、破解商店应用、绕过 DRM、规避付费、卸载系统核心组件、root、刷机或运行来路不明脚本。

## 执行前授权原则

ADB 命令会直接操作用户的 Quest 设备。回答 ADB 问题时，先说明命令作用、可能影响和可恢复方式，再询问用户希望“自己复制执行”还是“授权 agent 代为执行”。

- 如果用户选择自己执行：提供清晰命令、前置条件、预期输出和失败排查，不在本机代跑命令。
- 如果用户希望 agent 代为执行：必须先取得用户明确许可，再执行 ADB 命令；执行前复述将要运行的关键命令和影响范围。
- 对会修改设备状态的命令必须特别确认，例如 `adb install`、`adb uninstall`、`adb shell settings put/delete`、`adb shell am force-stop`、文件 `push/pull`、截图/录屏、重启设备。
- 对只读命令也应告知用途，例如 `adb devices`、`pm list packages`、`getprop`、`df -h`、`logcat -d`；导出日志前提醒可能包含账号、设备名、网络和路径信息。
- 未获得明确许可时，不要替用户执行任何 ADB 命令；可以先给命令和解释，让用户决定。

## 官方链接

- Android ADB 官方文档：`https://developer.android.com/tools/adb`
- Android SDK Platform Tools 下载页：`https://developer.android.com/tools/releases/platform-tools`
- Windows Oculus ADB Drivers：从 Meta 设备设置文档中的 `Oculus ADB Drivers` 链接进入；链接可能随 Meta 文档更新而变化。

涉及驱动下载地址、ADB 版本或最新要求时，优先让代理打开官方链接核实。开发者模式开启步骤统一读 `usage-tips.md`。

## 开发者模式前置

使用 ADB 前，Quest 通常需要先开启开发者模式并完成 USB debugging 授权。完整开启步骤、官方入口、账号/团队验证和常见失败排查统一读 `usage-tips.md` 的“如何开启开发者模式”。

## 安装 ADB

### 推荐方式：Android SDK Platform Tools

适合只需要命令行 ADB 的用户。

1. 打开 `https://developer.android.com/tools/releases/platform-tools`。
2. 下载对应系统的 SDK Platform Tools：
   - Windows：`platform-tools-latest-windows.zip`
   - macOS：`platform-tools-latest-darwin.zip`
   - Linux：`platform-tools-latest-linux.zip`
3. 解压到稳定目录，例如 Windows：`C:\platform-tools`。
4. 打开终端进入该目录，或把该目录加入系统 `PATH`。
5. 运行：

```text
adb version
adb devices
```

Windows 用户如果 `adb` 不是内部或外部命令，可以：

```text
cd C:\platform-tools
.\adb.exe version
.\adb.exe devices
```

### Windows 驱动

Windows 上如果 `adb devices` 看不到 Quest，按 Meta 官方设备设置文档安装 Oculus ADB Drivers：

1. 从 Meta 设备设置文档进入 `Oculus ADB Drivers` 下载页。
2. 下载并解压驱动。
3. 右键 `.inf` 文件，选择 Install。
4. 重新插拔 Quest，戴上头显确认 USB debugging。

不要从来历不明网盘或第三方安装包下载 ADB/驱动。优先使用 Google Platform Tools 和 Meta 官方驱动。

### Meta Quest Developer Hub

适合不想手动管理命令行、需要设备管理、日志、性能工具的用户。它不替代理解 ADB 基础；遇到命令行问题仍可回到 Platform Tools 排查。

## 连接与授权

```text
adb devices
adb kill-server
adb start-server
adb reconnect
```

- `device`：已授权，可以操作。
- `unauthorized`：戴上头显确认 USB 调试授权；必要时拔插线、重启 ADB。
- 空列表：换数据线、USB 口、驱动，确认不是只充电线。

多设备连接时先看序列号：

```text
adb devices -l
adb -s <serial> devices
```

后续命令可加 `-s <serial>` 指定设备。

## 解决连接国内 Wi-Fi 显示受限

适合：Quest 已经连上国内 Wi-Fi，局域网和部分网站可用，但系统提示 Wi-Fi 受限、无互联网或网络不可用。常见原因是 Android/Horizon OS 的联网检测地址在当前网络不可达，导致系统误判网络受限。

先提醒用户：这只能修复“联网检测误判”。如果 Wi-Fi 本身没有外网、DNS 错误、路由器断网、代理没有生效或 Meta 服务不可达，这些命令不会让网络凭空可用。

### 方式 A：改成更容易访问的联网检测地址

```text
adb shell settings put global captive_portal_http_url http://connect.rom.miui.com/generate_204
adb shell settings put global captive_portal_https_url https://connect.rom.miui.com/generate_204
adb shell settings put global captive_portal_fallback_url http://connect.rom.miui.com/generate_204
adb reboot
```

重启后重新连接 Wi-Fi，观察“受限”提示是否消失。如果用户不想重启，也可以先关闭再打开 Wi-Fi，但重启更干净。

### 方式 B：关闭联网检测

如果方式 A 无效，且用户确认网络实际可用，可关闭系统联网检测：

```text
adb shell settings put global captive_portal_mode 0
adb reboot
```

这会让系统不再依赖联网检测结果判断 Wi-Fi 是否可用。缺点是：以后连接需要网页登录认证的公共 Wi-Fi、酒店 Wi-Fi、校园网时，系统可能不会主动弹出门户登录页。

### 恢复默认设置

如果改完后网络表现异常，或用户需要恢复系统默认联网检测，可删除这些自定义项：

```text
adb shell settings delete global captive_portal_http_url
adb shell settings delete global captive_portal_https_url
adb shell settings delete global captive_portal_fallback_url
adb shell settings delete global captive_portal_mode
adb reboot
```

排查顺序：

1. 先确认 `adb devices` 显示 `device`。
2. 执行方式 A。
3. 重启后测试 Wi-Fi、浏览器、Meta Store。
4. 仍显示受限但实际能上网时，再考虑方式 B。

不要把这组命令描述成“科学上网”或“解锁 Meta 服务”的方案；它只处理 Android 联网检测/受限提示。

## 安装和覆盖安装 APK

```text
adb install "D:\Apps\example.apk"
adb install -r "D:\Apps\example.apk"
adb install -r -d "D:\Apps\example.apk"
```

- `adb install`：安装 APK。
- `-r`：保留数据覆盖安装，适合升级同签名应用。
- `-d`：允许降级安装，仅在确实需要回退版本时使用。
- 常见报错：
  - `INSTALL_FAILED_VERSION_DOWNGRADE`：版本号更低，确认是否需要 `-d`。
  - `INSTALL_FAILED_UPDATE_INCOMPATIBLE`：签名不一致，通常需要卸载旧版；先提醒数据风险。
  - `INSTALL_FAILED_INSUFFICIENT_STORAGE`：空间不足。
  - `INSTALL_PARSE_FAILED_NO_CERTIFICATES`：APK 签名或包损坏。

不要指导用户安装盗版、破解、绕过 DRM 的 APK。遇到这类请求时，改为推荐官方商店、App Lab、开源项目、用户自建 APK 或开发调试流程。

## 查询包名和卸载应用

```text
adb shell pm list packages
adb shell pm list packages | findstr keyword
adb shell pm list packages | grep keyword
adb uninstall com.example.app
adb uninstall -k com.example.app
```

- Windows 用 `findstr`，macOS/Linux 用 `grep`。
- `adb uninstall`：卸载用户安装的应用。
- `-k`：卸载但保留数据；只有用户明确需要保留数据时再用。
- 不要建议卸载 Meta/Horizon OS 核心包、系统服务、商店、账号、追踪、控制器相关包。无法判断包用途时先不要动。

## 启动和关闭 Quest 内应用

适合：用户已经知道应用包名，想从电脑端快速打开、重启或关闭头显内的 2D 应用、侧载应用、测试应用或自己开发的 APK。

先查包名：

```text
adb shell pm list packages
adb shell pm list packages | findstr keyword
adb shell pm list packages | grep keyword
```

启动应用：

```text
adb shell monkey -p com.example.app -c android.intent.category.LAUNCHER 1
```

`monkey` 方式适合大多数有启动入口的普通应用。把 `com.example.app` 换成真实包名。

如果用户知道具体 Activity，也可以用：

```text
adb shell am start -n com.example.app/.MainActivity
adb shell am start -n com.example.app/com.example.app.MainActivity
```

关闭或重启应用：

```text
adb shell am force-stop com.example.app
adb shell monkey -p com.example.app -c android.intent.category.LAUNCHER 1
```

查看当前前台应用，便于确认包名：

```text
adb shell dumpsys window | findstr mCurrentFocus
adb shell dumpsys window | grep mCurrentFocus
```

注意：

- `am force-stop` 会强制停止应用，可能中断下载、录制、同步或未保存进度。
- 不要强制停止 Meta/Horizon OS 核心服务、追踪、账号、商店、控制器、系统 UI 等组件。
- 如果 `monkey` 提示找不到启动入口，说明该包可能没有普通启动 Activity，或入口被系统/权限限制；不要用猜测命令乱启系统组件。

## 向 Quest 传文件

```text
adb shell mkdir -p /sdcard/Movies
adb push "D:\Movies\demo.mp4" /sdcard/Movies/
adb push "D:\Downloads\myfile.txt" /sdcard/Download/
adb shell ls -lah /sdcard/Movies
```

常用目录：

- `/sdcard/Download/`：下载文件、临时文件。
- `/sdcard/Movies/`：视频。
- `/sdcard/Pictures/`：图片。
- `/sdcard/Android/data/<package>/files/`：某些应用自己的文件目录，是否可用取决于应用和系统权限。

传输大视频时提醒用户保持头显亮屏或充电，避免线材松动。媒体文件传完后，用户可在文件管理器、浏览器下载目录、媒体播放器或对应应用内查找。

## 从 Quest 导出文件

```text
adb pull /sdcard/Download/ "D:\QuestBackup\Download"
adb pull /sdcard/Oculus/Screenshots/ "D:\QuestBackup\Screenshots"
adb pull /sdcard/Oculus/VideoShots/ "D:\QuestBackup\VideoShots"
adb pull /sdcard/Movies/demo.mp4 "D:\QuestBackup\"
```

截图和录屏目录会随系统版本变化；如果路径不存在，先用：

```text
adb shell ls /sdcard/
adb shell find /sdcard -iname "*.mp4"
adb shell find /sdcard -iname "*.jpg"
adb shell find /sdcard -iname "*.png"
```

## 截图与录屏

```text
adb shell screencap -p /sdcard/screen.png
adb pull /sdcard/screen.png "D:\QuestBackup\screen.png"
adb exec-out screencap -p > screen.png
adb shell screenrecord /sdcard/demo.mp4
adb pull /sdcard/demo.mp4 "D:\QuestBackup\demo.mp4"
```

`screenrecord` 通常有时长限制且不录系统音频；用于排障演示足够，不要承诺能完整录制所有应用内容。

## 日志和排障信息

```text
adb logcat -d > quest-log.txt
adb logcat -c
adb logcat
adb shell getprop ro.build.version.release
adb shell getprop ro.product.model
adb shell df -h
```

- `adb logcat -d > quest-log.txt`：导出当前日志，适合开发者排查崩溃。
- `adb logcat -c`：清空旧日志后复现问题，再导出更干净。
- `df -h`：看存储空间。
- 收集日志时提醒用户可能包含账号、路径、设备名、局域网信息，不要公开贴出完整日志。

## 重启与恢复连接

```text
adb reboot
adb reboot bootloader
adb disconnect
```

普通用户通常只需要 `adb reboot`。不要让用户进入 bootloader、刷机、解锁、root 或运行未知脚本，除非目标是明确的开发/维修场景且风险已说明。
