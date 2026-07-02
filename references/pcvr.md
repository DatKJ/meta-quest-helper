# PCVR

用于回答 Quest Link、Air Link、PCVR 硬件、路由器摆位、卡顿、黑屏和 SteamVR 问题。

## Choose A Path

- 有线 Quest Link：稳定，适合第一次排查 PCVR 基础问题。
- Air Link：官方无线方案，适合已有较好家庭 Wi-Fi 的用户。
- 其他串流应用：适合进阶调参用户，涉及价格和兼容性时先核实当前信息。

## PC Requirements

先确认：

- GPU 型号和显存。
- CPU、内存、系统版本。
- 显卡驱动版本。
- 游戏平台和目标游戏。
- 使用有线还是无线。
- 头显刷新率和渲染分辨率。

## Wireless Checklist

- PC 用网线连接路由器。
- Quest 靠近路由器或专用 AP。
- 优先使用 5 GHz 或 6 GHz Wi-Fi。
- 减少同频干扰和隔墙。
- 不把下载、网盘同步、直播推流和 PCVR 同时跑满。

## Stutter Troubleshooting

按顺序降低变量：

1. 先用有线 Link 测试 PC 性能是否足够。
2. 降低头显刷新率和渲染分辨率。
3. 降低游戏画质和 SteamVR 分辨率。
4. 关闭后台录屏、浏览器、同步工具和性能叠加层。
5. 更新显卡驱动、Quest 系统和 PC 端应用。
6. 无线时检查路由器摆位、频段、信道和 PC 有线连接。

## Black Screen Or No Audio

- 重启 Quest 和 PC。
- 换 USB 口或线材。
- 关闭再打开 Quest Link。
- 检查 Windows 默认音频设备。
- 检查显卡驱动和游戏平台运行状态。
- 只保留一个 VR 运行时做测试，避免多个运行时互相抢占。

## Wired Link Freezes Or Disconnects

典型现象：有线 Link 运行一段时间后黑屏、Link 画面冻结但音频和控制仍工作、约 30 分钟左右断连、断开后 PC 和 Quest 互相识别不到。

先做：

1. 用 Meta PC app 的 USB 测试确认线材和接口速度。
2. 换主板后置 USB 口，避免前置扩展坞和不稳定转接头。
3. 关闭 PC 的 USB 选择性暂停和设备管理器里的省电选项。
4. 更新或回退显卡驱动时，一次只改一个变量并记录版本。
5. 结束 Meta/Horizon/Oculus 相关进程后再重新打开 PC app；必要时重启 PC 和 Quest。
6. SteamVR 同时异常时，先单独测试 Quest Link 桌面，再测试 SteamVR，最后测试具体游戏。

判断方向：

- 只有高负载游戏会冻结：优先降低分辨率、刷新率、游戏画质和后台占用。
- USB 测试不稳定：优先换线、换口、去掉延长线。
- Air Link 也失败：检查 PC app、账号状态、同一局域网发现和防火墙。

## SteamVR And Runtime Conflicts

适合：SteamVR 不识别头显、Meta PC app 正常但 SteamVR 黑屏、切换游戏后运行时互相抢占。

1. 先确认 Quest Link 或 Air Link 本身可进入 PC 桌面。
2. 再启动 SteamVR，避免多个 VR 运行时同时抢占。
3. 更新 SteamVR、Meta PC app、显卡驱动和 Windows。
4. 游戏内运行时选项优先保持默认；改动 OpenXR/SteamVR 设置时逐项记录。
5. 如果某个游戏单独失败，先用一个轻量 VR app 做对照测试。

## Wireless Latency Spikes

适合：Steam Link、Air Link 或其他无线串流都出现网络延迟尖峰，平时低于 10 ms，偶尔跳到几十毫秒以上。

1. PC 必须用网线连接路由器。
2. Quest 尽量连接同一个 5 GHz 或 6 GHz SSID，靠近路由器测试。
3. 关闭路由器智能合并频段做对比。
4. 避免其他设备同时下载、同步、投屏或占满上行。
5. 更换 Wi-Fi 信道或换到干扰更少的位置。
6. 如果不同串流应用都卡，优先排查路由器、信道、距离和同频干扰，而不是只调某个 app。

## 2D PC Gaming And Gaze Cursor

适合：用 Quest 当大屏玩 2D PC 游戏时，gaze cursor 抢焦点、手柄/游戏手柄输入被切回键鼠布局。

1. 先确认目标是 2D 大屏游戏，不是 VR 游戏。
2. 优先在 PC 端确认游戏手柄输入稳定。
3. 在 Quest 端关闭不需要的手势输入或凝视选择选项，具体入口以当前系统为准。
4. 尝试固定窗口位置，减少头部准星停在游戏 UI 上。
5. 如果是某个游戏独有问题，检查游戏内控制器模式和窗口焦点。

## Sim Racing And Heavy PCVR Tuning

适合：Assetto Corsa、DCS、ETS2、赛车/飞行模拟等高负载场景。

- 优先保证稳定帧率，再追求最高分辨率。
- 先用中等分辨率、较低游戏画质和默认码率建立基线。
- 外部画面糊时，逐步提高渲染分辨率；车内仪表糊时，优先调字体、抗锯齿和清晰度。
- ASW/重投影开关要按游戏单独测试，不要一次改太多项。
- 记录 GPU 占用、显存、CPU 帧时间和网络/USB 指标，避免凭感觉调参。
