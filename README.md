<<<<<<< HEAD
[English](README-en.md) ←

# 借助 GitHub Actions 的 OpenWrt 在线集成自动编译.

## [![Build](https://img.shields.io/github/workflow/status/KFERMercer/OpenWrt/OpenWrt-CI/master?)](https://github.com/KFERMercer/OpenWrt/actions?query=workflow%3AOpenWrt-CI) [![Release](https://img.shields.io/github/release/KFERMercer/OpenWrt-CI?color=blue)](https://github.com/KFERMercer/OpenWrt-CI/releases)

支持自动定制固件, 自动调整依赖及生成配置文件, 无需上传配置. 兼容 [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede) 以及 OpenWrt trunk.

同时支持自动合并推送上游提交 (也就是自动更新), 直接把`merge-upstream.yml`放入`.github/workflows/`即可 (默认上游为 coolsnowwolf/lede, 高级玩家请自行改写).

感谢[P3TERX](https://github.com/P3TERX/Actions-OpenWrt)珠玉在前.

---

> ### 这个CI脚本和[P3TERX/Actions-OpenWrt](https://github.com/P3TERX/Actions-OpenWrt)的同样是云编译, 有什么不同?

这个 CI 脚本可以帮助你在你的 OpenWrt 分支下构建当前库的Op固件, 无需上传配置文件, 不依赖外挂配置脚本, 真正的一次配置终生使用.

P3TERX/Actions-OpenWrt 的优势在于, 其可以独立于文件库存在, 可以快速搭建起可用的编译配置; 同时对新手极其友好. 但是由于 OpenWrt make configure 自身机制的缘故, 生成的配置文件鲁棒性较差, 需要经常重新生成上传配置, 有形中加重了维护负担, 使得使用起来不是很`优雅`, **但是强烈建议基础薄弱的玩家使用.**

> ### 这个CI脚本适合哪些人?

- 正在维护自己的 OpenWrt 分支的大佬/初学者/玩家 (可以快速测试自己的代码)
- 伸手党
- 没有精力维持一个专用编译机的佛系人士

## 使用教程:

### 在一切开始前, 你需要的是:

- GitHub 账号
- 申请使用 GitHub Actions
- [基本的Git技能](https://www.liaoxuefeng.com/wiki/896043488029600)
- 自己的OpenWrt分支 ([Lean源](https://github.com/coolsnowwolf/lede)或者[官方源](https://github.com/openwrt/openwrt/))
- 脑子

### 相关文章: 作者-糖炒栗子 

- [面向小白的Github_Action使用workflow自动编译lean_openwrt教程](https://zhuanlan.zhihu.com/p/94402324)
- [关于Github Action自动编译Lean_Openwrt的配置修改问题](https://zhuanlan.zhihu.com/p/94527343)

### 1. 注册GitHub账号并开启GitHub Actions (自行搜索方法).

### 2. fork [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede) 或者 [OpenWrt trunk](https://github.com/openwrt/openwrt).

### 3. 上传`openwrt-ci.yml`和`merge-upstream.yml`到`/.github/workflows/`下.

### 4. 定制固件:

> 如果你希望定制你的固件:

代码里的注释部分详细介绍了如何在脚本中客制化你的固件. 简单来说, 你只需要解除注释相应行即可.

我已经准备一个[正确的编写示例](https://github.com/KFERMercer/OpenWrt-by-lean/blob/CI-demo/.github/workflows/openwrt-ci.yml), 此配置基于 Lean 最新代码, 开启了所有预先写好的定制选项, 同时已经[经过测试](https://github.com/KFERMercer/OpenWrt-by-lean/commit/d31390d3e7b5f178d4e3456d401ded557c207398/checks?check_suite_id=334570354)可用. 如果你缺乏对自己的信心, 可以随意借鉴.

### 5. 大功告成.

集成编译环境会自动开始编译. 现在返回你的库首页, 点击页面上方的`Actions`按钮就可以查看进度.

> ### 如何下载到编译完成的固件?

进入`Actions`标签页后, 如果相应的集成活动顺利完成 (显示为绿色), 点击页面右上方的`Artifacts`即可看到你的固件 (通常是一个压缩包). 点击即可开始下载.
=======
欢迎来到Lean的Openwrt源码仓库！
=
Welcome to Lean's  git source of OpenWrt and packages
=
中文：如何编译自己需要的 OpenWrt 固件
-
注意：
-
1. **不**要用 **root** 用户 git 和编译！！！
2. 国内用户编译前最好准备好梯子
3. 默认登陆IP 192.168.1.1, 密码 password

编译命令如下:
-
1. 首先装好 Ubuntu 64bit，推荐  Ubuntu  18 LTS x64

2. 命令行输入 `sudo apt-get update` ，然后输入
`
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3.5 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf
`

3. 使用 `git clone https://github.com/coolsnowwolf/lede` 命令下载好源代码，然后 `cd lede` 进入目录

4. ```bash
   ./scripts/feeds update -a
   ./scripts/feeds install -a
   make menuconfig
   ```

5. `make -j8 download v=s` 下载dl库（国内请尽量全局科学上网）


6. 输入 `make -j1 V=s` （-j1 后面是线程数。第一次编译推荐用单线程）即可开始编译你要的固件了。

本套代码保证肯定可以编译成功。里面包括了 R20 所有源代码，包括 IPK 的。

你可以自由使用，但源码编译二次发布请注明我的 GitHub 仓库链接。谢谢合作！
=

二次编译：
```bash
cd lede
git pull
./scripts/feeds update -a && ./scripts/feeds install -a
make defconfig
make -j8 download
make -j$(($(nproc) + 1)) V=s
```

如果需要重新配置：
```bash
rm -rf ./tmp && rm -rf .config
make menuconfig
make -j$(($(nproc) + 1)) V=s
```

编译完成后输出路径：/lede/bin/targets

特别提示：
------
1.源代码中绝不含任何后门和可以监控或者劫持你的 HTTPS 的闭源软件，SSL 安全是互联网最后的壁垒。安全干净才是固件应该做到的；

2.如有技术问题需要讨论，欢迎加入 QQ 讨论群：OP共享技术交流群 ,号码 297253733 ，加群链接: 点击链接加入群聊【OP共享技术交流群】：[点击加入](https://jq.qq.com/?_wv=1027&k=5yCRuXL "OP共享技术交流群")

3.想学习OpenWrt开发，但是摸不着门道？自学没毅力？基础太差？怕太难学不会？跟着佐大学OpenWrt开发入门培训班助你能学有所成
报名地址：[点击报名](http://forgotfun.org/2018/04/openwrt-training-2018.html "报名")

## Donate

如果你觉得此项目对你有帮助，可以捐助我们，以鼓励项目能持续发展，更加完善

### Alipay 支付宝

![alipay](doc/alipay_donate.jpg)

### Wechat 微信

![wechat](doc/wechat_donate.jpg)

------

English Version: How to make your Openwrt firmware.
-
Note:
--
1. DO **NOT** USE **ROOT** USER TO CONFIGURE!!!

2. Login IP is 192.168.1.1 and login password is "password".

Let's start!
---
First, you need a computer with a linux system. It's better to use Ubuntu 18 LTS 64-bit.

Next you need gcc, binutils, bzip2, flex, python3.5+, perl, make, find, grep, diff, unzip, gawk, getopt, subversion, libz-dev and libc headers installed.

To install these program, please login root users and type
`
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3.5 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib
`
in terminal

Third, logout of root users. And type this `git clone https://github.com/coolsnowwolf/lede` in terminal to clone this source.

After these please type `cd lede` to cd into the source.

Please Run `./scripts/feeds update -a` to get all the latest package definitions
defined in `feeds.conf` / `feeds.conf.default` respectively
and `./scripts/feeds install -a` to install symlinks of all of them into
`package/feeds/` .

Please use `make menuconfig` to choose your preferred
configuration for the toolchain and firmware.

Use `make menuconfig` to configure your image.

Simply running `make` will build your firmware.
It will download all sources, build the cross-compile toolchain,
the kernel and all choosen applications.

To build your own firmware you need to have access to a Linux, BSD or MacOSX system
(case-sensitive filesystem required). Cygwin will not be supported because of
the lack of case sensitiveness in the file system.

## Note: Addition Lean's private package source code in `./package/lean` directory. Use it under GPL v3.

## GPLv3 is compatible with more licenses than GPLv2: it allows you to make combinations with code that has specific kinds of additional requirements that are not in GPLv3 itself. Section 7 has more information about this, including the list of additional requirements that are permitted.
>>>>>>> ce326f078bede954be9ade6811409acca77b29e5
