# Meta Quest Helper

当前版本：`v1.1.2`

Meta Quest Helper 是一个面向中国大陆 Meta Quest 用户的 Agent Skill，用于帮助处理新机激活、首次配对、日常使用、ADB 操作、选购建议、PCVR、内容推荐和常见问题排障。

本 Skill 以中文为主，必要时保留英文产品名、App 名、设置路径和命令，方便用户对照设备界面操作。

## 能力范围

- Quest 新机激活、Meta Horizon App 配对和账号注意事项。
- 大陆首次激活网络方案，包括 UU、手机热点、路由器 Wi-Fi、SSTap 全局 UDP 热点等。
- 开发者模式、未知来源、SideQuest、Quest 助手、MQDH、中文语音输入法和 Quest 端网络工具说明。
- ADB 常用命令，包括安装 APK、传输文件、导出截图/录屏、采集日志、修复 Wi-Fi 受限提示、启动或关闭头显内应用。
- Quest 3S、Quest 3、Quest 2、Quest Pro、二手验机、配件、舒适度、头戴/头带选择。
- WebXR 网站、Quest 游戏和应用、健身/社交/影音/生产力/PCVR 内容推荐。
- Quest Link、Air Link、Steam Link、Virtual Desktop、SteamVR、延迟、黑屏、卡顿排查。
- 配对失败、商店空白、下载卡住、手柄配对、追踪丢失、边界异常、投屏失败、更新循环、晕动、起雾、发热和耗电等常见问题。

## 目录结构

```text
quest-helper/
  SKILL.md
  README.md
  LICENSE
  CHANGELOG.md
  references/
    activation.md
    adb.md
    buying.md
    content-recommendations.md
    pcvr.md
    troubleshooting.md
    usage-tips.md
```

`SKILL.md` 是 Agent Skill 主入口。OpenClaw、Codex、Claude Code、WorkBuddy 或其他兼容 Agent 工具应优先读取 `SKILL.md`，再按需要加载 `references/` 中的详细资料。

## 快速使用

适合用本 Skill 回答的问题包括：

- `Quest 3S 在大陆新机怎么激活？`
- `Quest 首次激活时网络不可达，怎么排查？`
- `未知来源不显示但我已经开了开发者模式。`
- `Quest 怎么用 adb 安装 apk？`
- `怎么把电影传到 Quest 里？`
- `Quest 3 和 3S 怎么选？`
- `Air Link 卡顿怎么排查？`
- `推荐几个 Quest 浏览器能玩的 WebXR 网站。`
- `Quest 连国内 Wi-Fi 显示受限，怎么用 ADB 修？`
- `无线 PCVR 应该先用 Steam Link 还是 Virtual Desktop？`

## 安全与合规

本 Skill 不协助违反法律法规、平台规则、授权规则、账号安全或支付规则的请求。

涉及网络环境、连接配置和路由器设置时，应提醒用户遵守所在地法律法规、服务条款、单位/学校网络规定和 Meta 平台政策。本 Skill 不推荐具体服务商或承诺可规避平台限制的服务。

ADB 命令会直接操作用户头显。代用户执行 ADB 命令前，应先说明命令作用、可能影响和恢复方式，并询问用户是自己复制执行，还是明确授权 Agent 代为执行。

## 许可证

MIT。详见 [LICENSE](LICENSE)。
