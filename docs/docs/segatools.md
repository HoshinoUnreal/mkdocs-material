---
comments: true
---

# SEGATOOLS 详细配置项目

<div align="center">
  <img src="/assets/segatools.png " alt="Image description">
</div>

!!! warning "观看前必读"

    本文档系对 [TeamTofuShop/segatools](https://gitea.tendokyu.moe/TeamTofuShop/segatools) 的配置文档进行翻译并附带笔者个人理解的产物。

    文档说明可能会因为笔者的理解能力而产生误差。
    
    如果您对文档内容有疑问，欢迎访问[原文链接](https://gitea.tendokyu.moe/TeamTofuShop/segatools/src/branch/develop/doc/config/common.md)或下方评论区讨论！

!!! info "TASOLLER (抬手乐) / TASOLLER PLUS (抬手乐普拉斯) / ZhouSensor (大四) 用户必读"

    如果您使用的控制器为TASOLLER（抬手乐）/TASOLLER PLUS（抬手乐普拉斯）/ZhouSensor（大四）的其中一种或者几种，请使用 fufubot 版本的 Segatools！

该文档描述了适用于所有游戏的 Segatools 配置设置。

键盘绑定设置使用[虚拟键代码](https://learn.microsoft.com/zh-cn/windows/win32/inputdev/virtual-key-codes)。
 ---

## **配置路径**

配置文件的默认路径是 `./segatools.ini`。

您可以通过修改环境变量 `SEGATOOLS_CONFIG_PATH` 来指定其他路径。

例如，您可以创建一个包含以下代码的 `start.bat` 文件，然后将 `segatools.ini` 复制为 `another_config.ini`，并在其中设置不同的 DNS 主机地址。

``` batch title="cmd"
set SEGATOOLS_CONFIG_PATH=.\another_config.ini
```

---

## **[aimeio]**

!!! note ""

    ### **`path`**

    指定第三方读卡器驱动程序 DLL 的路径。默认值为空（使用基于文本文件和键盘输入的内置模拟功能）。

    在之前的 Segatools 版本中，这一功能通过替换 Segatools 自带的 `aimeio.dll` 文件来实现。而在最新版本中，Segatools 不再附带单独的 `aimeio.dll` 文件（其功能现已集成到各个挂钩 DLL 中）。

---

## **[aime]**

控制 Aime 读卡器组件的模拟功能。

!!! note ""

    ### **`enable`**

    默认值：`1`

    启用 Aime 读卡器组件的模拟功能。禁用此选项可使用真实的 SEGA Aime 读卡器（COM 端口号因游戏而异）。

!!! note ""

    ### **`portNo`**

    默认值：`因游戏而异`

    设置用于 Aime 读卡器组件的 COM 端口。

!!! note ""

    ### **`highBaud`**

    默认值：`1`

    启用 Aime 读卡器的高波特率 115200（而非 38400）。某些游戏（如 CHUNITHM）需要此设置，而其他游戏（如 WACCA）则不需要。

!!! note ""

    ### **`gen`**

    默认值：`1`

    更改 Aime 读卡器的版本，这也会改变游戏中提供的 LED 信息。

    1. TN32MSEC003S H/W 版本 3.0 / TN32MSEC003S F/W 版本 1.2

    2. 837-15286 / 94

    3. 837-15396 / 94

!!! note ""

    ### **`aimePath`**

    默认值：`DEVICE\aime.txt`

    指向包含经典 Aime IC 卡 ID 的文本文件路径。

    !!! warning "注意"

        Aime 卡ID为20位阿拉伯数字。

!!! note ""

    ### **`aimeGen`**

    默认值：`1`

    如果指定路径 `aimePath` 的文件不存在，是否生成一个随机的 Aime ID。

!!! note ""

    ### **`felicaPath`**

    默认值：`DEVICE\felica.txt`

    指向包含 FeliCa 电子现金卡 IDm 序列号的文本文件路径。

!!! note ""

    ### **`felicaGen`**

    默认值：`0`

    如果指定路径 `felicaPath` 的文件不存在，是否生成一个随机的 FeliCa ID。

!!! note ""

    ### **`scan`**

    默认值：`0x0D`（VK_RETURN）

    虚拟键码。如果按住此按钮，则模拟的 IC 卡读卡器会模拟其附近的 IC 卡。可以模拟多种不同的 IC 卡；模拟的具体卡片类型取决于配置的卡 ID 文件是否存在。

## **[vfd]**
控制 VFD GP1232A02A FUTABA 组件的模拟功能。

!!! note ""

    ### **`enable`**
    默认值：`1`

    启用 VFD 模拟功能。禁用此选项可使用真实的 VFD GP1232A02A FUTABA 组件（COM 端口号因游戏而异）。

!!! note ""

    ### **`portNo`**

    默认值：`因游戏而异`

    设置用于 VFD 组件的 COM 端口。

!!! note ""

    ### **`utfConversion`**

    默认值：`0`

    将 VFD 中的字符串从各自的编码转换为 UTF，这样控制台输出在非日本区域设置下会正确显示。

---

## **[amvideo]**

控制内置于 Segatools 的 amvideo.dll 模拟程序。这个程序通常存在于 SEGA 操作系统镜像中，负责更改屏幕分辨率和方向。

!!! note ""

    ### **`enable`**

    默认值：`1`

    启用 amvideo.dll 模拟程序。禁用此选项可使用真实的 amvideo.dll 文件。请注意，您必须安装正确的注册表设置，并且必须使用与您的 GPU 供应商匹配的 amvideo.dll 版本（因为这些 DLL 使用供应商特定的 API）。

---

## **[clock]**

控制 Windows 时间 API 的钩子。

!!! note ""

    ### **`timezone`**

    默认值：`1`

    将系统时区设置为 JST（日本标准时间）。如果系统时区不是 JST，SEGA 游戏可能会出现奇怪的故障。除非存在实现上的 bug，否则不应禁用此钩子，但如果需要，仍然提供了禁用的选项。

!!! note ""

    ### **`timewarp`**

    默认值：`0`

    实验性的时间扭曲钩子，用于跳过硬编码的服务器维护期间。这会导致游戏内报告不正确的时间。

    !!! example "实验性功能注意"

        针对这个问题已经有更好的解决方案，且此功能可能很快会被移除。

!!! note ""

    ### **`writeable`**

    默认值：`0`
    
    允许游戏调整系统时钟和时区设置。通常情况下应保持为 0，但如果需要，提供了此选项。
