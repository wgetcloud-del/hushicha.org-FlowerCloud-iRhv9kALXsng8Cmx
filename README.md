


---


　　大家好，我是痞子衡，是正经搞技术的痞子。今天痞子衡给大家介绍的是**MCUXpresso for VS Code开发环境搭建及SDK工程导入**。


　　MCUXpresso IDE（包括其前身 LPCXpresso IDE、Kinetis Design Studio）是恩智浦软件团队持续开发了十多年的免费集成开发环境，现在功能已经相当完善，IDE 里面菜单与功能选项无数，每一项都凝结了软件团队的心血。


　　近年来 Visual Studio Code 在嵌入式领域的用户越来越多（主要原因是其通用性，不与任何一家 MCU 原厂深度绑定，且第三方插件众多，生态强大，新功能支持更灵活），为了给恩智浦用户更灵活的开发体验，恩智浦于2023年7月正式推出了 MCUXpresso for Visual Studio Code 插件，把 MCUXpresso IDE 里对 NXP MCU 的支持以及一些核心功能都带到了 Visual Studio Code 里。


　　今天痞子衡要介绍的是 MCUXpresso for VS Code 开发环境搭建以及如何导入恩智浦 SDK 工程开发调试，算是 MCUXpresso for VS Code 入门第一步。


### 一、MCUXpresso for VS Code概述


　　在恩智浦官网 [MCUXpresso for VS Code 主页](https://github.com) 我们可以看到其原理框图（下图下半部分），我们将其和 MCUXpresso IDE 原理框图（下图上半部分）放在一起比较，会很容易发现它们的异同。


　　相同的地方是，都能做源代码编辑、工程组织管理，GNU 编译工具链集成、调试器支持。不同的地方在于 MCUXpresso IDE 有自己原生的各种调试组件及其特色的 Linker 文件图形化编辑器，而 MCUXpresso for VS Code 除了依托于 VS Code 的插件市场以及 Git 源代码版本管理，还增强了对 Zephyr 相关的支持（West、KConfig、Device Tree）。


![](https://raw.githubusercontent.com/JayHeng/pzhmcu-picture/master/cnblogs/MCUX_VSC_QSG_bg.png)


### 二、搭建开发环境


　　现在开始搭建开发环境，毕竟是 VS Code 的插件，那么首先就是安装一个 VS Code，需要从如下微软官网下载安装，痞子衡安装得是 V1\.96\.2 版本。



> * VS Code主页：[https://code.visualstudio.com/](https://github.com)


　　打开 VS Code，在左侧工具栏 "Extensions" 里搜索 MCUXpresso for VS Code 即可找到本文主角，直接点 "install" 安装（痞子衡安装的插件是 v24\.10\.78 版本）。安装完成之后，即可在工具栏里看到 MCUXpresso 快捷入口。


![](https://raw.githubusercontent.com/JayHeng/pzhmcu-picture/master/cnblogs/MCUX_VSC_QSG_ext_setup.png)


　　此时只是搭好了 MCUXpresso for VS Code 基本代码编辑与工程管理环境，但是工程开发所需的编译调试工具还没有就位。为了方便用户一键安装全部依赖工具，恩智浦额外提供了 [MCUXpresso Installer (Windows版本)](https://github.com)，下载这个工具，双击打开，利用它进一步安装编译调试等工具（分别安装 MCUXpresso SDK Developer、LinkServer、SEGGER J\-Link）。



> * Note: 如果本地已经已经安装了 Git、CMake、Python 等工具，MCUXpresso Installer 会识别并使用，不会重复安装。


![](https://raw.githubusercontent.com/JayHeng/pzhmcu-picture/master/cnblogs/MCUX_VSC_QSG_installer.png)


### 三、导入SDK工程


　　MCUXpresso for VS Code 下支持两种不同的工程导入方式，一种是 Git Repo 方式（恩智浦已经将 SDK 部署到 github 了），另一种是本地 SDK ZIP 包方式（与 [《MCUXpresso IDE下SDK工程导入》](https://github.com) 方法差不多），本文主要介绍后一种。


　　我们可以从 [恩智浦 SDK builder](https://github.com):[wgetcloud全球加速服务机场](https://wa7.org) 网站下载一个软件包 SDK\_2\_16\_000\_MIMXRT1060\-EVKB.zip（Toolchain 需包含 GCC），然后在 VS Code 界面 Import Repository 里选择 **LOCAL ARCHIVE**，选中下载好的软件包，Location 里设置 SDK 解压路径，点击 Import。


![](https://raw.githubusercontent.com/JayHeng/pzhmcu-picture/master/cnblogs/MCUX_VSC_QSG_sdk1.png)


　　这时候 SDK\_2\_16\_000\_MIMXRT1060\-EVKB.zip 已经被导入到当前 VS Code 里，下一步利用 Import Example from Repository 创建一个具体例程，Template 选项里可以看到 SDK 包里全部例程，这里选择 demo\_apps/hello\_world，再在 Location 里设置用户例程路径，点击 Create。


![](https://raw.githubusercontent.com/JayHeng/pzhmcu-picture/master/cnblogs/MCUX_VSC_QSG_sdk2.png)


　　现在我们就拥有了一个 VS Code 下的 hello\_world 工程，在左侧 PROJECTS 下面可以看到工程源文件，可以对工程进行编译，此时给 RT1060\-EVKB 板卡通上电插上调试器（板载 DAP\-Link 或者外接 J\-Link 均可），就可以直接下载调试了。


![](https://raw.githubusercontent.com/JayHeng/pzhmcu-picture/master/cnblogs/MCUX_VSC_QSG_sdk3.png)


　　至此，MCUXpresso for VS Code开发环境搭建及SDK工程导入痞子衡便介绍完毕了，掌声在哪里\~\~\~


### 欢迎订阅


文章会同时发布到我的 [博客园主页](https://github.com)、[CSDN主页](https://github.com)、[知乎主页](https://github.com)、[微信公众号](https://github.com) 平台上。


微信搜索"**痞子衡嵌入式**"或者扫描下面二维码，就可以在手机上第一时间看了哦。


![](https://raw.githubusercontent.com/JayHeng/pzhmcu-picture/master/wechat/pzhMcu_qrcode_258x258.jpg)


