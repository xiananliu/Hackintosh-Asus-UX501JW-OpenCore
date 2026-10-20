# Hackintosh ASUS ZenBook Pro UX501JW — OpenCore · macOS Monterey

ASUS ZenBook Pro UX501JW (Haswell) 黑苹果 EFI 配置，OpenCore 引导，macOS Monterey 21H1320 实机验证。

## 硬件配置

| 项目 | 规格 |
|---|---|
| 笔记本 | ASUS ZenBook Pro UX501JW |
| CPU | Intel Core i7-4720HQ (Haswell, HM87) |
| 核显 | Intel HD Graphics 4600 |
| 独显 | NVIDIA GTX 960M 2GB（macOS 下屏蔽，SSDT-Disable_GPU_PEG0）|
| 内存 | 16GB DDR3 |
| 声卡 | Realtek ALC668 + B&O ICEpower |
| 无线/BT | Intel 7260（AirportItlwm + IntelBluetoothFirmware）|
| 屏幕 | 15.6" 1080p（SAMSUNG 156HL01-102，核显注入覆盖 EDID）|

## 功能状态

- ✅ 声卡：扬声器 + 耳机全正常（layout 27，boot-args `alcid=27 alcverbs=1`）
- ✅ 内屏 HD4600 加速（Metal 正常）
- ✅ 键盘背光 Fn+F3/F4（AsusSMC + SSDT-ASUS，见注意事项）
- ✅ Fn 亮度键 / 电池 / 睡眠 / USB / Intel WiFi & BT
- ❌ HDMI 输出：本批次板线 HDMI 接 GTX 960M 独显，Monterey 无 Maxwell 驱动，无解（见 detail）
- ❓ mini DP / Thunderbolt：未实测（理论上 miniDP→HDMI 主动转接头值得一试，核显 config 处于原生 DP 状态）

## 使用说明

1. BIOS：DVMT 128M，关闭 Secure Boot，显卡模式保持默认（支持 NVIDIA Optimus）
2. 引导后 OpenCore 菜单：光标停在 macOS 记录上按 `Ctrl+Enter` 设为默认启动
3. config 内 SMBIOS：MacBookPro11,5（OpenCore Utility 生成，未混用 Apple 真机信息）

## 注意事项

- **键盘背光**：若 Fn+F3/F4 弹出"打叉"图标或亮度无效，是 macOS"键盘亮度自动调节"策略在接管背光（环境光变暗或关闭该选项即恢复），不是故障。
- **HDMI**：经实测本机 HDMI 板线接独显，核显侧试遍连接器映射均无热插拔电平反应；同型号 4K 屏批次（moharram82 配置 0A2E0008）HDMI 可用，故属板线批次差异。独显在本任务上无救济路径。
- **声卡**：全部靠 `alcid=27 alcverbs=1`（boot-args 保留完整），请勿删；旁路备份见 `config.plist` 的 NVRAM>Add。
- **鼠标光标内存**：`framebuffer-cursormem = 0x00900000`（9MB）为 Haswell Glitchs 修复。

## Credits

- [OpenCore](https://github.com/acidanthera/OpenCorePkg)、[Lilu 系列](https://github.com/acidanthera)（WhateverGreen / VirtualSMC 等）
- [AppleALC](https://github.com/acidanthera/AppleALC)
- [AsusSMC](https://github.com/hieplpvip/AsusSMC)（ASUS Fn/背光/ALS）
- [Firefly917/Hackintosh_Asus-UX501JW_Mojave](https://github.com/firefly917/Hackintosh_Asus-UX501JW_Mojave)、[moharram82/Asus-ZenBook-Pro-UX501JW-Hackintosh](https://github.com/moharram82/Asus-ZenBook-Pro-UX501JW-Hackintosh)（同型号为参考）

> 本仓库仅用于个人装机共享。所有 kext/驱动版权归各自作者。
