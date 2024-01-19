**闭源驱动** | ~[开源驱动](README_mainline.md)~

# Actions-rax3000m-NAND
使用 GitHub Actions 在线编译定制 CMCC RAX3000M NAND version 的 immortalwrt-mt798x 固件

## 固件特性
使用 [hanwckf](https://github.com/hanwckf) 大佬的 [immortalwrt-mt798x](https://github.com/hanwckf/immortalwrt-mt798x) 项目仓库，'openwrt-21.02' 分支源码编译，无线使用 mtwifi 原厂无线驱动，内核版本 5.4.x

并加入 [237大佬](https://github.com/padavanonly) 的 [高功率无线eeprom](https://github.com/GD-Slime/immortalwrt-mt798x/commit/f7e8c89835f263d0ef07a005d29af456b923a5b8) commit

项目详情：[immortalwrt-mt798x项目介绍](https://cmi.hanwckf.top/p/immortalwrt-mt798x)

添加软件包
`luci-app-mosdns, luci-app-adguardhome, luci-app-argon-config, luci-app-autoreboot, luci-app-passwall, luci-app-ttyd, luci-app-upnp, luci-theme-argon`
等（请自行到config文件查看）

加入由 [1715173329 天灵](https://github.com/1715173329) 使用 js 重写，[237大佬](https://www.right.com.cn/forum/?364126) 适配硬件 QoS 的 [luci-app-eqos-mtk](https://github.com/padavanonly/immortalwrt-mt798x/commit/7c8019ce4bcb1a79c01c517b62e49f059ca70049)

## 使用说明
在 Actions 选择该工作流手动点击 Run workflow 执行编译，等待固件编译完成上传至 releases 发布即可下载

### 配置说明
- 默认 LAN IP 已更改为 `192.168.123.1`，可在 `scripts/diy.sh` 处修改

- 需要取消集成或添加其他软件包可在 `configs/rax3000m-emmc_mtksdk.config` 处参考注释内容自行修改或添加配置选项

- 默认构建使用 OpenWrt 原生 luci 无线控制界面，如需使用 MTK SDK 无线控制界面 (luci-app-mtk) 请在 Run workflow 时取消勾选 “Use mtwifi-cfg”，或在 workflow 配置文件中将 `USE_MTWIFI_CFG` 中 `default: true` 的 true 改为 false，重新编译刷入使用

- 默认构建 eeprom 替换为 H3C NX30 Pro 提取版本（来自 [237大佬](https://www.right.com.cn/forum/?364126) 提取）以增大无线功率，**原厂 eeprom 无线信号 2.4G: 23dBm, 5G: 22dBm；替换 nx30pro_eeprom 后 2.4G: 25dBm, 5G: 24dBm**

~~路由器进入 uboot 需要手动设置本机 IP 192.168.1.100 网关 192.168.1.1 DNS 192.168.1.1，~~ 新版 custom U-Boot 已支持 DHCP，浏览器输入 `192.168.1.1` 进入 Web-UI 刷写固件，所有文件可在 https://firmware.download.immortalwrt.eu.org/uboot/mediatek 获取

## Credits
- [XiaoBinin/Actions-immortalwrt](https://github.com/XiaoBinin/Actions-immortalwrt)
- [ImmortalWrt](https://github.com/immortalwrt/immortalwrt)
- [hanwckf/immortalwrt-mt798x](https://github.com/hanwckf/immortalwrt-mt798x)
- [lgs2007m/immortalwrt-mt798x-rax3000m-emmc](https://github.com/lgs2007m/immortalwrt-mt798x-rax3000m-emmc)
- [GL-iNet](https://github.com/gl-inet)
- [padavanonly](https://github.com/padavanonly)
- [Microsoft Azure](https://azure.microsoft.com)
- [GitHub Actions](https://github.com/features/actions)
- [OpenWrt](https://github.com/openwrt/openwrt)
- [tmate](https://github.com/tmate-io/tmate)
- [mxschmitt/action-tmate](https://github.com/mxschmitt/action-tmate)
- [csexton/debugger-action](https://github.com/csexton/debugger-action)
- [Cowtransfer](https://cowtransfer.com)
- [WeTransfer](https://wetransfer.com/)
- [Mikubill/transfer](https://github.com/Mikubill/transfer)
- [softprops/action-gh-release](https://github.com/softprops/action-gh-release)
- [ActionsRML/delete-workflow-runs](https://github.com/ActionsRML/delete-workflow-runs)
- [dev-drprasad/delete-older-releases](https://github.com/dev-drprasad/delete-older-releases)
- [peter-evans/repository-dispatch](https://github.com/peter-evans/repository-dispatch)

## License

[MIT](https://github.com/P3TERX/Actions-OpenWrt/blob/main/LICENSE) © [**P3TERX**](https://p3terx.com)
