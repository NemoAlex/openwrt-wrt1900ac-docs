关于无线模块驱动的更新

# 更新驱动

OpenWrt/DD-WRT 的 WRT1900AC 系列的无线驱动是由 [mwlwifi 项目](https://github.com/kaloz/mwlwifi) 提供的。

OpenWrt 15.05 正式版携带的无线驱动版本是 10.3.0.3。这是一个存在许多问题的版本，驱动作者在后续的版本更新中已经修复了大量问题，大幅度提高了性能。

2016.1.6 更新：[mwlwifi-bin 项目](https://github.com/NemoAlex/mwlwifi-bin) 会持续跟进编译对应 OpenWrt 稳定版（当前：15.05 正式版）的驱动。本项目不再重复提供。

**目前编译的版本，仅仅适用于 OpenWrt 15.05 Chaos Calmer 正式版。**

**注意：可以用于 Nemo 0.1 版 和 1.2 版，不适用于 Nemo 1.1 版**

# 安装方法

想办法上传安装文件到路由器上，使用 scp 或者什么别的工具。也可以[参考这里](https://github.com/NemoAlex/openwrt-wrt1900ac-docs/wiki/%E5%AE%89%E8%A3%85%E5%92%8C%E6%9B%B4%E6%96%B0%E8%BD%AF%E4%BB%B6) 的方式，使用 Git。

这里以安装 10.3.0.14 为例，给出一个通用的方法：

安装 git

    opkg update
    opkg install git-http

下载项目，注意这里选择 /tmp 目录是因为空间够大，不过重启以后会被系统清除。

    cd /tmp
    git clone --depth 1 https://github.com/NemoAlex/mwlwifi-bin

安装

    cd mwlwifi-bin
    opkg install kmod-mwlwifi_3.18.20\+10.3.0.14-20151107-1_mvebu.ipk

成功以后，重启路由器。

一切正常的话，运行 `strings /lib/modules/*.*/mwlwifi.ko | grep "^10.3"` 可以看到目前的驱动版本。