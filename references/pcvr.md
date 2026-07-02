# PCVR、串流与延迟排查

## 先确认

- PC 显卡、CPU、内存。
- 是否使用笔记本，是否独显直连。
- 路由器型号、Wi-Fi 5/6/6E、Quest 与路由器距离。
- PC 到路由器是有线还是 Wi-Fi。
- 使用 Quest Link、Air Link、Steam Link 还是 Virtual Desktop。
- 游戏来自 Meta PC、SteamVR 还是其他平台。
- 问题类型：卡顿、延迟、马赛克、黑屏、SteamVR 报错、USB 断连、手柄/追踪抖动。

## 方案选择

无线串流软件优先推荐 Steam Link：它免费、接入简单，对大多数只想玩 SteamVR 的 Quest 用户已经够用。Virtual Desktop 更适合愿意付费、追求更多画质/码率/编码细调选项，或 Steam Link/Air Link 体验不理想的进阶用户。

### 有线 Quest Link

适合：想要稳定、路由器一般、能接受线缆。

注意：

- 使用支持数据传输的 USB 3 线。
- 测试 Link 带宽。
- 笔记本确认使用独显。
- 换 USB 口时优先试主板后置 USB 3 口，避免前置口、扩展坞和只充电线。
- 不要边充电边依赖劣质线高负载工作。

### Air Link

适合：想用 Meta 官方无线方案，PC 和路由器条件较好。

建议：

- PC 有线连接路由器。
- Quest 使用 5 GHz/6 GHz。
- 路由器与 Quest 同房间。
- 从较低码率开始，再逐步提高。

### Steam Link

适合：主要玩 SteamVR，想简单接入 Steam 生态，希望先用免费方案完成无线 PCVR 的大多数用户。

建议：

- 无线 PCVR 首选先试 Steam Link。
- 先确认 SteamVR 能正常运行，再调串流质量。
- 如果只是玩常见 SteamVR 游戏，Steam Link 通常已经够用，不必一开始就购买 Virtual Desktop。
- 若遇到画质、延迟、控制器映射或兼容性问题，再与 Air Link 或 Virtual Desktop 对比。

### Virtual Desktop

适合：愿意购买第三方软件并细调码率、编码、画质的用户，或 Steam Link/Air Link 无法满足需求的进阶用户。

提醒：购买前先试 Steam Link；再核实 Virtual Desktop 当前兼容性、账号地区、商店可用性、价格和退款规则。

## 网络布局

理想布局：

```text
PC --有线--> 路由器 --5GHz/6GHz--> Quest
```

不理想布局：

```text
PC --Wi-Fi--> 路由器 --Wi-Fi--> Quest
```

电脑和 Quest 都走无线时，延迟和抖动会明显增加。

## 卡顿定位

区分四类问题：

- PC 性能不足：游戏本身掉帧，降低游戏画质或分辨率。
- 编码压力：显卡编码器满载，降低码率/刷新率。
- Wi-Fi 抖动：画面马赛克、延迟尖峰，优化路由器和频段。
- 平台链路问题：SteamVR/Meta Link 软件异常，重启服务或更新驱动。

排查顺序：

1. 用本地显示器确认 PC 游戏不掉帧。
2. 降低 SteamVR supersampling/渲染分辨率、串流码率和刷新率。
3. PC 改有线。
4. Quest 靠近路由器。
5. SteamVR 异常时按 SteamVR -> 头显 -> PC 的顺序重启。
6. 切换 Air Link/Steam Link/Virtual Desktop 对比。
7. 更新显卡驱动、Meta Quest Link、SteamVR 和头显固件。

## SteamVR 与黑屏

- SteamVR 报错或识别异常：先重启 SteamVR，再重启头显，最后重启 PC；避免一次改很多设置。
- 黑屏：检查线缆/无线连接、GPU 驱动、Meta Quest Link、SteamVR、头显固件和笔记本独显输出。
- 追踪抖动：排查光线、反光面、摄像头清洁、USB 带宽和 Wi-Fi 抖动。
- 性能差：先降 supersampling/渲染分辨率，再降游戏画质、刷新率和码率。
- Link 线断连：换 USB 3 口、换线、关闭省电策略，确认线材不是只支持充电。

## 常见建议

- 不要把“能上外网”和“PCVR 不卡”混为一谈。PCVR 主要看局域网质量和 PC 性能。
- 串流路由器可以不负责全屋上网，但应给 PC 和 Quest 提供稳定局域网。
- 高码率不是越高越好；稳定帧率和低抖动更重要。
- 90 Hz/120 Hz 对 PC 和网络要求更高，新手先从 72/80/90 Hz 稳定开始。
- VR 开发或调试时要频繁真机测试；桌面预览无法可靠暴露晕动、交互距离、手柄姿态和性能掉帧问题。
