<h1 align="center">General-EFI-for-OpenCore-Config</h1>
<h3 align="center">通用OpenCore EFI配置文件</h3>
<br>

## 概览 / Overview

辅助快速安装黑苹果的模板

Template for Quick installation of Hackintosh

## 免责声明 / Disclaimer

你的保修将完全失效。如果您有任何疑虑，请在使用我的项目之前先进行一些研究。我对任何损失均不负责，包括但不限于 Kernel Panic、设备无法启动或无法正常工作、硬件损坏或数据丢失、原子弹爆炸、第三次世界大战、SCP 基金会无法避免的 CK 级现实重构等。

Your warranty is now void. Please do some research if you have any concerns before utilizing my project. I am not responsible for any loss, including but not limited to Kernel Panic, device fail to boot or can not function normally, storage damage or data loss, atomic bombing, World War III, The CK-Class Restructuring Scenario that SCP Foundation can not prevent, and so on.

## 必读参考资料 / Refrence

- [dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [dortania's OpenCore Post Install Guide](https://dortania.github.io/OpenCore-Post-Install/)
- [dortania Getting Started with ACPI](https://dortania.github.io/OpenCore-Post-Install/)
- [dortania opencore multiboot](https://github.com/dortania/OpenCore-Multiboot)
- [WhateverGreen Intel HD Manual](https://github.com/acidanthera/WhateverGreen/blob/master/Manual/FAQ.IntelHD.en.md)
- `Configuration.pdf` and `Differences.pdf` in each OpenCore releases.
- [daliansky/OC-little](https://github.com/daliansky/OC-little)
- [OpenCore 简体中文参考手册 (非官方)](https://oc.skk.moe)

**务必阅读上述参考资料**

**No seriously, PLEASE read those.**

## 需求和依赖 / Requirement

### 基本需求 / Basic

- 一台已经安装好 macOS 的机器，用于制作 macOS 安装器和编译本项目（但是Windows PC也可以做到）

A macOS machine (optional): to create the macOS installer and build the EFI. (But windows PC can do the same)

- 一个容量大于等于 16 GiB 的 U 盘

Flash drive, 16GB or more, for the above purpose.

- 编辑 plist 文件的工具 [PlistEDPlus](https://github.com/ic005k/PlistEDPlus)

[PlistEDPlus](https://github.com/ic005k/PlistEDPlus) to edit plist files on Windows.

- 用于修补和编辑 ACPI 的工具 [MaciASL](https://github.com/acidanthera/MaciASL)

[MaciASL](https://github.com/acidanthera/MaciASL) for patching ACPI tables and editing ACPI patches.

- 在 macOS 下挂载 EFI 分区的工具 [MountEFI](https://github.com/corpnewt/MountEFI)

[MountEFI](https://github.com/corpnewt/MountEFI) to quickly mount EFI partitions under macOS.

- 用于诊断的 [IORegistryExplorer](https://developer.apple.com/downloads)

[IORegistryExplorer](https://developer.apple.com/downloads) for diagnosis.

- **仅用于** 诊断的 [HackinTool](https://github.com/headkaze/Hackintool)，大部分内置的补丁和工具已经过时，不再适用

[HackinTool](https://github.com/headkaze/Hackintool) for diagnosis ONLY. Most of the built-in patches are outdated.

- 可在Windows操作系统环境下简单快捷地定制USB端口的工具 [USBToolBox Beta](https://github.com/USBToolBox/tool)。

[USBToolBox Beta](https://github.com/USBToolBox/tool) a tool that can easily and quickly customize USB port in Windows operating system.

- 耐心和时间，以及自主学习能力。如果你是第一次进行黑苹果，这尤为重要

Patience and time, as well as autonomous learning ability. especially if this is your first time Hackintosh-ing.

### 硬件修改 / Hardware Modification

#### 固态硬盘 / SSD

三星 PM981/PM981a/PM991 和 镁光 2200S **完全** 无法使用，务必更换至少一块 SSD 硬盘。

Samusung PM981/PM981a/PM991 and Micron 2200S is not supported AT ALL. Make sure to switch at least one SSD.

#### 无线网卡 / Wireless Card

It is recommended to use Broadcom wireless network card to obtain **Better** performance and use native functions about「Apple Ecology」(I mean, 100x FASTER!)

建议使用博通无线网卡以获得 **更好** 的性能和使用原生的关于「苹果生态」的功能（更好，指速度快 **100 倍**）

### 升级或降级BIOS版本 / Update or Downgrade BIOS Version

推荐使用特定版本的 BIOS 固件以获得最佳的使用体验。但是我们通常推荐使用最新版BIOS固件。

A specific version of BIOS firmware is recommended for the best experience. But we usually recommend the latest version of BIOS firmware.

从主板厂商的支持网站上下载BIOS固件。

Download BIOS at Motherboard manufacturer Support Website. 

### 修改BIOS设置 / BIOS Settings

禁用 / Disabled
* Fast Boot～快速启动
* VT-d(can be enabled if you set DisableIoMapper Quirks to YES)～VT-d（如果DisableIOMapper Quirks设置为YES，则可以启用）
* CSM～CSM 兼容性支持模块
* Thunderbolt (Temporarily disabled)～雷雳（暂时禁用）
* Intel SGX～英特尔SGX
* Intel Platform Trust～英特尔平台信任
* CFG Lock(MSR 0xE2 write protection)～CFG锁（MSR 0xE2写保护）（必须关闭，如果找不到该选项，则在OpenCore的config-内核-> Quirks下启用与CFG Lock相关选项）
* Secure Boot～安全启动
* Parallel Port～并口
* Serial/COM Port～串行/COM端口

启用 / Enabled
* VT-x～VT-x
* UEFI启动模式。请不要使用Legacy（UEFI startup mode. Please don't use Legacy）
* 硬盘模式改AHCI。不能用IDE和RST RAID。（Hard disk mode changed to AHCI. IDE and RST Raid cannot be used）
* Above 4G decoding～大于4G地址空间解码
* Hyper-Threading～超线程
* Execute Disable Bit～执行禁用位
* EHCI/XHCI Hand-off～EHCI / XHCI接手控制
* OS type: Windows 8.1/10 UEFI Mode～操作系统类型：Windows 8.1 / 10 UEFI模式
* DVMT Pre-Allocated(iGPU Memory): DVMT预分配（iGPU内存）：64MB及以上 （64MB and above）
* Legacy RTC Device～传统RTC设备

## 其他信息 / Other Information

OpenCore关于Kernel的Quirks XhciPortLimit 在macOS Big Sur 11.3及更新版本中失效。

OpenCore Quirks XhciPortLimit for Kernel is invalid in macOS Big Sur 11.3 and later.

请在安装 macOS Big Sur 11.3以及更新版本前，定制USB端口。

Please customize the USB Port before installing MacOS Big Sur 11.3 or later.

在安装完 macOS Big Sur 11.3以及更新版本后，请禁用config-Kernel-Quirks-XhciPortLimit 。

After installing macOS Big Sur 11.3 and later, disable config-Kernel-Quirks-XhciPortLimit .

- 具体详细注意事项和推荐参数内容都通过“#”注释方法写在了config文件内，请自行参考吧。

The detailed notes and recommended parameters are written in the config file through the "#" annotation method, please refer to it.

待补充……

To be added……

## 笔记本用户 / Laptops Users

- HP惠普笔记本用户

HP Laptops Users

Kernel->Quirks->LapicKernelPanic->True

UEFI->Quirks->UnblockFsConnect->True

- Dell戴尔笔记本用户

Dell Laptops Users

Kernel->Quirks->CustomSMBIOSGuid->True

PlatformInfo->Quirks->UpdateSMBIOSMode->Custom

## 鸣谢 / Gratitude

- Apple macOS
- Acidanthera Team
- Dortania‘s OpenCore Install Guide

etc......

## 捐赠 / Donation

捐赠本项目 **并不是必需的**。但是如果我的项目对你有所帮助，为什么不考虑一下给我买杯咖啡呢？

Donating to this project is OPTIONAL. But feel free to buy me a coffee if you appreciate my works.

## 维护者 / Maintainer

© [Miracle樱乃.](https://github.com/Miracle-Sakuno), Released under the [MIT License](./LICENSE) .<br>
Authored and maintained by Miracle樱乃. with help from contributors ([list](https://github.com/Miracle-Sakuno/General-EFI-for-OpenCore-Config/graphs/contributors)).

> GitHub [@Miracle樱乃.](https://github.com/Miracle-Sakuno) · Twitter [@Miracle樱乃.](https://twitter.com/Miracle_Sakuno) · Telegram Channel [@Rabbit House](https://t.me/RabbitHouse_i)

此文档暂时归档，若有其他维护者请勿改动

### 注意：本人公开的社交账号仅为此Github，Twitter和Telegram频道，以及本人QQ账号为：2112074157。除以上四个本人专用账号之外，其他任何以我的名义来发布消息的都是骗子，注意核实
### 尤其注意此人QQ账号：1063995989，长时间故意盗用本人身份发布各类不实消息，请各位注意核实，并帮助我举报他
### 感谢各位支持

Note: my social account is only for GitHub, twitter and telegraph channels, and my QQ account is 2112074157. In addition to the above four personal accounts, any other person who publishes information in my name is a liar. Pay attention to verification

Pay special attention to this person's QQ account: 1063995989. He deliberately embezzles his identity and publishes all kinds of false news for a long time. Please pay attention to verification and help me report him

Thank you for your support
