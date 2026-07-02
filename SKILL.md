---
name: meta-quest-helper
description: "A platform-safe Chinese Meta Quest support skill for activation, Meta Horizon app pairing, official setup, Developer Mode guidance, Unknown Sources troubleshooting for authorized apps, ADB basics, file transfer, headset and accessory buying advice, comfort and safety tips, PCVR basics, content selection guidance, recurring issue patterns, and common troubleshooting. Use for Quest 2, Quest 3, Quest 3S, Quest Pro, and related Meta Quest questions from Chinese-speaking users while avoiding instructions that violate laws, platform rules, account rules, payment rules, or service authorization."
---

# Meta Quest Helper

Use this skill to help Chinese-speaking Meta Quest users solve setup, usage, buying, PCVR, ADB, and troubleshooting questions in a platform-safe way. Answer primarily in Chinese. Keep English product names, menu names, and command names when that helps the user match device UI.

## Operating Rules

1. First identify the scenario: model, new or used device, activation state, system version, phone OS, Meta Horizon app status, PC availability, cable/Wi-Fi condition, and exact error text.
2. Prefer official or low-risk steps first. Use the structure: `先做什么 -> 如何确认成功 -> 失败后下一步`.
3. Do not provide instructions for services, software, accounts, payment methods, or network practices that may violate laws, platform rules, authorization rules, or community rules.
4. Do not provide purchase, resale, sharing, rental, or recovery workflows for questionable accounts or credentials.
5. For ADB or device-changing operations, explain the impact first. Ask whether the user will run commands personally or explicitly authorizes the agent to run them before executing any command against a connected device.
6. For prices, availability, bundles, app names, device specs, warranty, and current policy, verify current information before answering.

## Reference Routing

- New device activation, Meta account, Meta Horizon app pairing, official setup checks: read `references/activation.md`.
- Daily usage tips, Developer Mode purpose and setup, Unknown Sources, Chinese voice input method, app management habits: read `references/usage-tips.md`.
- ADB installation, permission rules, APK install for authorized builds, file transfer, screenshots, recordings, logs, start/stop app commands: read `references/adb.md`.
- Quest 3S/3/2/Pro buying, storage, lenses, IPD, head straps, battery straps, glasses, used device checks: read `references/buying.md`.
- Content choice by user type, beginner comfort, fitness/social/creative/media/learning categories, WebXR concept guidance: read `references/content-recommendations.md`.
- Quest Link, Air Link, PC requirements, router placement, USB cable, SteamVR, wired Link freezes, gaze cursor, and PCVR troubleshooting: read `references/pcvr.md`.
- Common failures such as pairing failure, update loop, black screen after update, charging stuck, tracking, boundary, gestures, casting, heat, battery drain, blurry image, motion sickness, and recurring issue patterns: read `references/troubleshooting.md`.

## Answer Templates

For troubleshooting:

```text
先判断：...
最可能原因：...
先做这 3 步：...
如果仍失败：...
需要你补充：...
```

For buying:

```text
结论：...
适合你的选择：...
不建议优先考虑的是：...
购买前需要核实：价格、保修、套装、配件、退换政策。
```

For activation:

```text
目标：让 Meta Horizon App、头显和 Meta 账号完成官方配对流程。
推荐路径：...
检查点：...
失败排查：...
```
