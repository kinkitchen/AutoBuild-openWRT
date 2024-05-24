感谢Hyy2001X的源码！全部贡献来自各位大佬！！！

支持的 OpenWrt 源码: `coolsnowwolf/lede`、`immortalwrt/immortalwrt`、`openwrt/openwrt`、`lienol/openwrt`

**提示**: 文档中的 **TARGET_PROFILE** 为编译的设备名称(代号), 例如: `d-team_newifi-d2`、`asus_rt-acrh17`、`x86_64`
   
**TARGET_PROFILE** 本地获取方法如下:
   
① 执行`make menuconfig`, 进行设备选择后即可保存并退出
   
② 在源码目录执行`egrep -o "CONFIG_TARGET.*DEVICE.*=y" .config | sed -r 's/.*DEVICE_(.*)=y/\1/'`
   
或`grep 'TARGET_PROFILE' .config` 均可获取 **TARGET_PROFILE**

## 一、定制固件(可选)

1. **Fork** 该仓库, 并进入你自己的`AutoBuild-Actions`仓库, **下方所有操作都将在你的`AutoBuild-Actions`仓库下进行**, 可以 **Clone** 到本地操作

   建议使用`Github Desktop`或`Notepad--`进行编辑和提交操作 [[Github Desktop](https://desktop.github.com/)] [[Notepad--]([https://notepad-plus-plus.org/downloads/](https://gitee.com/cxasm/notepad--/releases/tag/v2.11))]

2. 编辑`Configs`目录下的配置文件, 配置文件的命名一般为**TARGET_PROFILE**, 若配置文件不存在则需要在本地生成并上传

3. 编辑`.github/workflows/***.yml`文件, 修改`第 7 行 name:`, 填写一个便于识别的名称 `e.g. NEWIFI D2`

4. 编辑`.github/workflows/***.yml`文件, 修改`第 32 行 CONFIG_FILE:`, 填写你添加到`Configs`目录下的配置名称

5. 根据需求编辑 [Scripts/AutoBuild_DiyScript.sh](./Scripts/AutoBuild_DiyScript.sh)
   
添加软件包、其他定制选项请在 `Firmware_Diy()` 函数中编写, `Scripts`目录下的其他文件无需修改

**Scripts/AutoBuild_DiyScript.sh: Firmware_Diy_Core() 函数中的变量:**
```
   Author 作者名称, AUTO: [自动识别]
   
   Author_URL 自定义作者网站或域名, AUTO: [自动识别]

   Default_Flag 固件标签 (名称后缀), 适用不同配置文件, AUTO: [自动识别]

   Default_IP 固件 IP 地址

   Default_Title 终端首页显示的额外信息

   Short_Fw_Date 简短的固件日期, true: [20210601]; false: [202106012359]

   x86_Full_Images 额外上传已检测到的 x86 虚拟磁盘镜像, true: [上传]; false: [不上传]
   
   Fw_MFormat 自定义固件格式, AUTO: [自动识别]

   Regex_Skip 输出固件时丢弃包含该内容的文件

   AutoBuild_Features 自动添加 AutoBuild 固件特性, 建议开启

   注: 禁用某功能请将变量值修改为 false, 开启则为 true

```

## 二、编译固件

   **手动编译** 点击上方工具栏中的`Actions`选项, 在左侧选择设备,点击右方`Run workflow`再点击`绿色按钮`即可开始编译

   **Star 一键编译** 编辑`.github/workflows/***.yml`文件, 删除注释`#`符号并提交修改, 单击或双击点亮右上角的 **Star** ⭐按钮即可一键编译

```
  #watch:
  #  types: [started]
```
   **定时编译** 编辑`.github/workflows/***.yml`文件, 删除注释`#`符号, 并按需修改时间并提交修改 [Corn 使用方法](https://www.runoob.com/w3cnote/linux-crontab-tasks.html)
```
  #schedule:
  #  - cron: 0 8 * * 5
```
   **临时修改固件 IP 地址** 该功能仅在**手动编译**生效, 点击`Run workflow`后即可输入 IP 地址
   
   **使用其他 [.config] 配置文件** 点击`Run workflow`后即可选择`Configs`目录下的配置文件名称

## 三、部署云端日志(可选)

1. 下载本仓库中的 [Update_Logs.json](https://github.com/Hyy2001X/AutoBuild-Actions/releases/download/AutoUpdate/Update_Logs.json) 到本地 (如果有)

2. 以 **JSON** 格式编辑本地的`Update_Logs.json`

3. 手动上传修改后的`Update_Logs.json`到`Github Release`

4. 在本地执行`autoupdate --fw-log`测试

## 使用一键更新固件脚本(可选)

   首先需要打开`TTYD 终端`或者使用`SSH`, 按需输入下方指令:

   更新固件: `autoupdate`

   使用镜像加速更新固件: `autoupdate -P`

   更新固件(不保留配置): `autoupdate -n`
   
   强制刷写固件(危险): `autoupdate -F`
   
   强制下载并刷写固件: `autoupdate -f`

   更新脚本: `autoupdate -x`
   
   打印运行日志:  `autoupdate --log`

   查看脚本帮助: `autoupdate --help`

## 鸣谢

   - [Lean's Openwrt Source code](https://github.com/coolsnowwolf/lede)

   - [P3TERX's Blog](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

   - [ImmortalWrt's Source code](https://github.com/immortalwrt)

   - [eSir 's workflow template](https://github.com/esirplayground/AutoBuild-OpenWrt/blob/master/.github/workflows/Build_OP_x86_64.yml)
   
   - [[openwrt-autoupdate](https://github.com/mab-wien/openwrt-autoupdate)] [[Actions-OpenWrt](https://github.com/P3TERX/Actions-OpenWrt)]

   - 测试与建议: [CurssedCoffin](https://github.com/CurssedCoffin) [Licsber](https://github.com/Licsber) [sirliu](https://github.com/sirliu) [神雕](https://github.com/teasiu) [yehaku](https://www.right.com.cn/forum/space-uid-28062.html) [缘空空](https://github.com/NaiHeKK) [281677160](https://github.com/281677160)
