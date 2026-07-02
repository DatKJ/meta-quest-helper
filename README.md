# Meta Quest Helper

一个面向中文 Meta Quest 用户的 Agent Skill，用于帮助处理官方激活、首次配对、日常使用、ADB 操作、选购建议、PCVR、内容选择和常见问题排障。

当前版本：`v1.1.0`

内容采用平台友好的合规边界，优先提供官方流程、可信来源和可恢复的低风险排障步骤。

## 能力范围

- Quest 新机激活、Meta Horizon App 配对和官方设置检查。
- 开发者模式、未知来源、中文语音输入法和授权 APK 测试。
- ADB 常用命令：安装授权 APK、传输文件、导出截图和录屏、采集日志、启动或关闭应用。
- Quest 3S、Quest 3、Quest 2、Quest Pro、二手验机和配件选购。
- 头戴方案、眼镜用户、运动空间、清洁和新手避坑。
- PCVR、Quest Link、Air Link、SteamVR 和卡顿排查。
- 内容类型推荐、WebXR 概念说明和舒适度建议。

## 目录结构

```text
meta-quest-helper/
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

Agent 工具应优先读取 `SKILL.md`，再按问题类型加载 `references/` 中的资料。

## 合规边界

本 Skill 不协助任何违反法律法规、平台规则、服务条款、授权协议或社区规则的请求。涉及账号、安全验证、支付、网络、设备系统和 ADB 操作时，应优先采用官方流程、可信来源和可恢复的低风险步骤。

## 许可证

MIT。详见 [LICENSE](LICENSE)。
