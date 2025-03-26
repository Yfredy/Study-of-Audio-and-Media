# Study of Audio and Media

## 音视频进阶

## 深入理解Android

## git教程

### git安装Mac

1. 通过App Store安装Xcode, 会自动安装Git, 或使用Homebrew安装：`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
2. 打开终端, 输入以下命令：`git add .`
3. 输入以下命令：`git commit -m "COMMIT_MESSAGE"`
4. 输入以下命令：`git push origin master`

## Android调试方法

### adb调试

ADB(Android Debug Bridge)是一个通用命令行工具, 可让你与模拟器实例或连接的 Android 设备进行通信。以下是详细的 ADB 调试教程：

#### 1. 安装 ADB
- **Windows 系统**
    - 从 [Android SDK Platform-Tools](https://developer.android.com/studio/releases/platform-tools) 页面下载最新的平台工具压缩包。
    - 解压下载的压缩包到你选择的目录, 例如 `C:\Android\platform-tools`。
    - 将该目录添加到系统的环境变量 `PATH` 中。具体步骤为：右键点击“此电脑”, 选择“属性”, 点击“高级系统设置”, 在“系统属性”窗口中选择“环境变量”, 在“系统变量”中找到 `Path` 变量, 点击“编辑”, 然后添加解压后的目录路径。
- **macOS 系统**
    - 可以使用 Homebrew 进行安装, 打开终端并运行以下命令：
        ```bash
        brew install --cask android-platform-tools
        ```
    - 或者手动下载平台工具压缩包, 解压后将 `platform-tools` 目录添加到 `PATH` 环境变量中。在终端中编辑 `~/.bash_profile` 或 `~/.zshrc` 文件, 添加如下内容：
        ```bash
        export PATH=$PATH:/path/to/platform-tools
        ```
    - 保存文件后, 运行 `source ~/.bash_profile` 或 `source ~/.zshrc` 使配置生效。
- **Linux 系统**
    - 在 Ubuntu 或 Debian 系统中, 可通过以下命令安装：
        ```bash
        sudo apt-get install android-tools-adb
        ```

#### 2. 启用设备的 USB 调试模式
- **安卓设备**
    - 打开设备的“设置”应用。
    - 找到“关于手机”或“关于设备”选项。
    - 连续点击“版本号”7 次, 开启开发者选项。
    - 返回“设置”主界面, 进入“开发者选项”, 开启“USB 调试”。
- **安卓模拟器**：大多数安卓模拟器默认开启了 USB 调试模式, 无需额外设置。

#### 3. 连接设备
- 使用 USB 数据线将安卓设备连接到电脑。
- 打开终端或命令提示符, 输入 `adb devices` 命令。如果设备连接成功且 USB 调试已开启, 你将看到设备的序列号以及设备状态为 `device`, 例如：
    ```plaintext
    List of devices attached
    0123456789ABCDEF    device
    ```

#### 4. 常用 ADB 命令
- **设备信息类**
    - `adb devices`：列出所有连接的设备。
    - `adb get-serialno`：获取设备的序列号。
    - `adb get-state`：获取设备的状态(device、offline 等)。
    - `adb shell getprop ro.product.model`：获取设备的型号。
- **文件操作类**
    - `adb push <本地文件路径> <设备目标路径>`：将本地文件复制到设备中。例如：`adb push C:\test.txt /sdcard/`
    - `adb pull <设备文件路径> <本地目标路径>`：将设备中的文件复制到本地。例如：`adb pull /sdcard/test.txt C:\`
    - `adb shell ls <设备目录路径>`：查看设备指定目录下的文件列表。
- **应用操作类**
    - `adb install <APK 文件路径>`：安装 APK 文件到设备。例如：`adb install C:\app.apk`
    - `adb uninstall <应用包名>`：卸载设备上的应用。例如：`adb uninstall com.example.app`
    - `adb shell pm list packages`：列出设备上安装的所有应用包名。
- **系统操作类**
    - `adb shell reboot`：重启设备。
    - `adb shell poweroff`：关闭设备。
    - `adb shell input text <文本内容>`：在设备上模拟输入文本。例如：`adb shell input text "Hello"`
    - `adb shell input keyevent <按键码>`：模拟按键操作。例如, `adb shell input keyevent KEYCODE_HOME` 模拟按下 Home 键。

#### 5. 断开连接
完成调试后, 你可以直接拔掉 USB 数据线断开设备连接。也可以在终端中输入 `adb kill-server` 命令停止 ADB 服务。

参考链接
[Android系统调试工具大全: 解密adb、dumpsys、procrank等神器](https://blog.csdn.net/u011897062/article/details/134574362)

### adb调试

1. Android开发中, 调试是一个非常重要的环节, 本文将介绍一些常用的Android系统调试工具, 包括adb、logcat、procrank、dumpsys、dmesg、top、free、df、trace、pm、am等, 帮助开发者更好地排查和解决问题。Android开发中, 调试是一个非常重要的环节。Android Debug Bridge(ADB)是一款强大的命令行工具, 提供了与Android设备进行通信和调试的功能。本文将介绍adb的基本使用方法, 包括连接设备、安装应用、卸载应用、文件传输等, 帮助开发者更好地排查和解决问题。
2. 连接设备。首先, 确保你的Android设备已连接到开发机上, 并且已启用USB调试模式。然后, 打开终端或命令提示符窗口, 输入以下命令以检查设备是否被正确识别：
    ```bash
    adb devices
    ```
    如果设备列表中显示了连接的设备ID, 则表示连接成功。
3. 安装应用。使用adb可以轻松地安装应用程序到Android设备上。在终端或命令提示符窗口中, 导航到应用程序安装文件所在的目录, 并执行以下命令：
    ```bash
    adb install your_app.apk
    ```
    其中, your_app.apk是你要安装的应用程序文件名。安装过程中, 你可以在设备上看到应用程序的安装进度。
4. 卸载应用。如果你想从设备上移除某个应用程序, 可以使用以下命令：
    ```bash
    adb uninstall com.example.app
    ```
    其中, com.example.app是应用程序的包名。卸载过程中, 你可以在终端或命令提示符窗口中看到卸载的结果信息。
5. 文件传输。使用adb可以方便地在Android设备和开发机之间传输文件。以下是一些常用的文件传输命令：
    将文件从开发机复制到设备：
    ```bash
    adb push local_file_path /device/path
    ```
    其中, local_file_path是本地文件的路径, /device/path是设备存储的目标路径。
    将文件从设备复制到开发机：
    ```bash
    adb pull /device/path local_file_path
    ```
    其中, /device/path是设备上文件的路径, local_file_path是要保存文件的本地路径。注意：在执行文件传输命令之前, 确保设备已连接并处于可用状态。

### logcat调试
logcat是Android平台上的一项日志记录工具, 可以通过它来查看Android系统和应用程序的日志信息。本文将详细介绍logcat命令及参数的含义, 以及如何使用它来查看日志信息, 帮助开发者更好地排查和解决问题。logcat是Android平台上的一款命令行工具, 主要用于查看系统和应用程序的日志信息。以下是一些常用的logcat命令及参数：
1. 查看所有日志信息：
    ```bash
    adb logcat
    ```
    此命令可以查看所有级别的日志信息, 包括调试、信息、警告、错误等。
2. 查看特定标签的日志信息：
    ```bash
    adb logcat -s TAG
    ```
    其中, TAG是日志信息的标签名称。此命令可以筛选出指定标签的所有日志信息。
3. 显示调试级别的日志信息：
    ```bash
    adb logcat -v debug
    ```
    此命令可以查看调试级别的日志信息, 包括VERBOSE、DEBUG、INFO、WARN、ERROR等级别的信息。
4. 保存日志信息到文件：
    ```bash
    adb logcat -f logfile.txt
    ```
    此命令可以将日志信息保存到指定的文件中。
5. 清除日志缓存：
    ```bash
    adb logcat -c
    ```
    此命令可以清除日志缓存, 以便查看最新的日志信息。
6. 过滤指定级别的日志信息：
    ```bash
    adb logcat *:D
    ```
    此命令可以筛选出调试级别(DEBUG)及以上级别的日志信息。你可以根据需要将级别替换为V(VERBOSE)、I(INFO)、W(WARN)或E(ERROR)。
7. 使用正则表达式过滤日志信息：
    ```bash
    adb logcat -v brief | grep "keyword"
    ```
    此命令可以使用grep命令结合正则表达式来过滤日志信息。将"keyword"替换为你想要搜索的关键词。这样可以帮助你快速找到包含特定关键词的日志。
8. 查看特定进程的日志信息：
    ```bash
    adb logcat --pid=PID
    ```
    其中, PID是进程ID。此命令可以查看特定进程生成的日志信息。
9. 查看特定线程的日志信息：
    ```bash
    adb logcat --pid=PID --tid=TID
    ```
    其中, TID是线程ID。此命令可以查看特定线程生成的日志信息。
10. 格式化输出日志信息：
    ```bash
    adb logcat -v json
    ```
    此命令可以以JSON格式输出日志信息, 便于后续处理和分析。
11. 查看所有日志信息：
    ```bash
    adb logcat -v time
    ```
    此命令可以查看所有级别的日志信息, 并按照时间顺序显示。
12. 在日志信息中, 每一行都包含了日期、时间、标签、进程ID和消息等信息。通过这些信息, 我们可以了解Android系统和应用程序的运行状态, 从而更好地进行调试和分析工作。

### procrank
procrank是一个用于查看系统内存使用情况的命令行工具, 运行在设备侧的 shell 环境下,用来输出进程的内存快照,便于有效的观察进程的内存占用情况。
1. 包括如下内存信息:
    - `VSS`:`Virtual Set Size` 虚拟耗用内存大小(包含共享库占用的内存)
    - `RSS`:`Resident Set Size` 实际使用物理内存大小(包含共享库占用的内存)
    - `PSS`:`Proportional Set Size` 实际使用的物理内存大小(比例分配共享库占用的内存)
    - `USS`:`Unique Set Size` 进程独自占用的物理内存大小(不包含共享库占用的内存)
    - 注意:
        - `USS` 大小代表只属于本进程正在使用的内存大小,进程被杀死后会被完整回收;
        - `VSS/RSS` 包含了共享库使用的内存,对查看单一进程内存状态没有参考价值;
        - `PSS` 是按照比例将共享内存分割后,某单一进程对共享内存区的占用情况。
2. 使用procrank, 执行procrank前需要先让终端获取到root权限
    ```bash
    su
    ```
    命令格式:
    ```bash
    procrank [ -W ] [ -v | -r | -p | -u | -h ]
    ```
    常用指令说明:
    - `-v`:按照 `VSS` 排序
    - `-r`:按照 `RSS` 排序
    - `-p`:按照 `PSS` 排序
    - `-u`:按照 `USS` 排序
    - `-R`:转换为递增[递减]方式排序
    - `-w`:只显示 working set 的统计计数
    - `-W`:重置 working set 的统计计数
    - `-h`:帮助
3. 按照 VSS 降序排列输出内存快照:
    ```bash
    procrank -v
    ```
    默认procrank输出是通过PSS排序。
4. procrank命令及参数, procrank命令主要用于显示系统中各个进程的内存使用情况, 包括内存占用量、进程名等信息。以下是一些常用的procrank命令及参数：
    查看系统内存使用情况：
    ```bash
    procrank
    ```
    此命令可以列出系统中各个进程的内存使用情况, 包括`进程名`、`PID`、`Vss`、`Rss`、`Pss`等信息。
5. 以H级别的信息显示系统内存使用情况：
    ```bash
    procrank -h
    ```
    通过加上`-h`参数, 可以显示更详细的内存使用信息, 包括进程的地址空间(Vss)、RAM使用(Rss)、共享内存使用(Pss)等信息。
6. 按照内存使用量排序显示：
    ```bash
    procrank -o
    ```
    加上`-o`参数可以按照内存使用量从高到低进行排序显示, 帮助用户快速找出内存占用较大的进程。
7. 检索指定内容信息, 查看指定进程的内存占用状态,命令格式如下:
    ```bash
    procrank | grep [cmdline | PID]
    ```
    其中`cmdline`表示需要查找的应用程序名, `PID`表示需要查找的应用进程。输出`systemUI`进程的内存占用状态:
    ```bash
    procrank | grep “com.android.systemui”
    ```
    或者:
    ```bash
    procrank | grep 3396
    ```
8. 跟踪进程内存状态, 通过跟踪内存的占用状态,进而分析进程中是否存在内存泄露场景。使用编写脚本的方式,连续输出进程的内存快照,通过对比 USS 段,可以了解到此进程是否有内存泄露。
    示例:输出进程名为 com.android.systemui 的应用内存占用状态,查看是否有泄露:
    ```bash
    1、编写脚本 test.sh
    #!/bin/bash
    while true;do
    adb shell procrank | grep “com.android.systemui”
    sleep 1
    done
    ```
    2、通过 adb 工具连接到设备后,运行此脚本: `./test.sh`

9. 如何使用procrank查看系统内存使用情况, 要使用procrank查看系统的内存使用情况, 首先需要将设备连接到开发机, 并打开终端或命令提示符窗口。然后, 在命令行中输入相应的procrank命令及参数即可。
    以下是一个简单的例子, 演示如何使用procrank查看系统的内存使用情况：
    ```bash
    procrank -h
    ```
    此命令可以显示更详细的内存使用信息, 帮助开发者全面了解系统中各个进程的内存占用情况。

### dumpsys
dumpsys是一个用于查看Android系统的各种信息的命令行工具, 运行在设备侧的 shell 环境下,提供系统中正在运行的服务状态信息功能。正在运行的服务是指 Android binder机制中的服务端进程。dumpsys 输出打印的条件:
1. 只能打印已经加载到 ServiceManager中的服务;
2. 如果服务端代码中的 dump 函数没有被实现,则没有信息输出。
3. dumpsys命令及参数
    - dumpsys命令主要用于显示Android系统的各种信息, 包括CPU、内存、网络、电池等。以下是一些常用的dumpsys命令及参数：
    1. 查看系统的所有信息：
    ```bash
    dumpsys
    ```
    此命令可以列出系统的各种信息, 包括CPU、内存、网络、电池等信息。
    2. 查看Dumpsys包含服务列表
    ```bash
    dumpsys -l
    ```
    作用:输出dumpsys所有可打印服务信息,开发者可以关注需要调试服务的名称。
    3. 查看指定服务的信息：
    ```bash
    dumpsys <service>
    ```
    通过指定服务名, 可以只查看特定服务的信息, 例如：
    ```bash
    dumpsys battery
    ```
    此命令可以查看电池状态信息。
    4. 输出指定服务和应有进程的信息
    ```bash
    dumpsys [servicename] [应用名]
    ```
    示例:输出服务名为 meminfo,进程名为 com.android.systemui 的内存信息,执行命令:
    ```bash
    dumpsys meminfo com.android.systemui
    ```
    注意:服务名称是大小写敏感的,并且必须输入完整服务名称。
    5. 将结果保存到文件中：
    ```bash
    dumpsys > <file>
    ```
    通过将结果重定向到文件中, 可以将dumpsys输出的信息保存下来, 例如：
    ```bash
    dumpsys > dump.txt
    ```
    此命令可以将dumpsys输出的信息保存到`dump.txt`文件中。
6. 如何使用dumpsys查看Android系统的各种信息
    - 要使用dumpsys查看Android系统的各种信息, 首先需要将设备连接到开发机, 并打开终端或命令提示符窗口。然后, 在命令行中输入相应的dumpsys命令及参数即可。

    以下是一个简单的例子, 演示如何使用dumpsys查看电池状态：
    ```bash
    dumpsys battery
    ```
    此命令可以查看设备的电池状态信息, 包括电池电量、充电状态等。

### dmesg
dmesg是一个用于查看系统启动时的日志信息和内核消息的命令行工具, 本节将详细介绍dmesg命令及参数的含义, 以及如何使用它来查看系统启动时的日志信息和内核消息。
1. dmesg命令及参数
    - dmesg命令主要用于显示系统启动时的日志信息和内核消息, 包括硬件检测、驱动加载、内存分配、系统调用等信息。以下是一些常用的dmesg命令及参数：
    1. 查看系统启动时的日志信息和内核消息：
    ```bash
    dmesg
    ```
    此命令可以列出系统启动时的日志信息和内核消息, 包括硬件检测、驱动加载、内存分配、系统调用等信息。
    2. 仅查看最近的N行日志：
    ```bash
    dmesg -n N
    ```
    通过加上-n参数并指定N的值, 可以仅查看最近的N行日志, 例如：
    ```bash
    dmesg -n 10
    ```
    此命令可以仅查看最近的10行日志信息和内核消息。
       1. 按照时间戳排序显示：
    ```bash
    dmesg -T
    ```
    加上-T参数可以按照时间戳从新到旧的顺序进行排序显示, 帮助用户快速找出最近出现的问题。
    3. 查看特定级别的日志信息：
    除了上述介绍的基本用法之外, dmesg还有其他一些用法和参数, 使其更灵活和强大。
    查看特定级别的日志信息：可以通过加上不同的参数来过滤特定级别的日志信息, 例如只查看错误级别的日志：
    ```bash
    dmesg -l err
    ```
    或只查看警告级别的日志：
    ```bash
    dmesg -l warn
    ```
    实时查看日志信息：通过结合使用dmesg命令和tail命令, 可以实时查看最新的日志信息, 例如：
    ```bash
    dmesg -w | tail
    ```
    此命令会持续输出最新的日志信息, 方便进行实时监控。
    4. 将结果保存到文件中：
    通过将结果重定向到文件中, 可以将dmesg输出的日志信息保存下来, 例如：
    ```bash
    dmesg > dmesg.log
    ```
    此命令可以将dmesg输出的日志信息保存到dmesg.log文件中。
    5. 显示可读的时间戳：通过加上-H参数, 可以显示易读的时间戳格式, 例如：
    ```bash
    dmesg -H
    ```
    此命令会将时间戳转换为易读的格式, 方便阅读和理解。
    6. dmesg -c命令用于清除内核环缓冲区中的日志信息。当执行该命令时, 它会将当前内核环缓冲区中的内容显示出来, 并清空该缓冲区。
    ```bash
    dmesg -c
    ```
    执行命令后, 终端会显示当前内核环缓冲区中的日志信息, 并将其清空。
    请注意, 执行dmesg -c命令会清除内核环缓冲区中的所有日志信息, 因此在执行该命令之前请确保您已经记录或备份了需要保留的日志信息。
2. 要使用dmesg -c命令, 请按照以下步骤操作：
    - 打开终端或命令提示符窗口。
    - 输入以下命令并按Enter键执行：
    ```bash
    dmesg -c
    ```
    执行命令后, 终端会显示当前内核环缓冲区中的日志信息, 并将其清空。
    请注意, 执行dmesg -c命令会清除内核环缓冲区中的所有日志信息, 因此在执行该命令之前请确保您已经记录或备份了需要保留的日志信息。
3. 如何使用dmesg查看系统启动时的日志信息和内核消息
    - 要使用dmesg查看系统启动时的日志信息和内核消息, 首先需要打开终端或命令提示符窗口。然后, 在命令行中输入相应的dmesg命令及参数即可。
4. 以下是一个简单的例子, 演示如何使用dmesg查看系统启动时的日志信息和内核消息：
    ```bash
    dmesg
    ```
    此命令可以列出系统启动时的日志信息和内核消息, 帮助开发者了解系统启动过程中的各种信息。

### top、free、df
在Android系统开发和运维中, 了解系统的内存、CPU和磁盘使用情况是非常重要的。本文将介绍三个常用的Linux命令：top、free和df, 在Android系统中的应用以及如何使用它们来查看系统的内存、CPU和磁盘使用情况。
1. top命令
    - top命令是一个动态监视系统资源使用情况的命令行工具, 可以实时显示进程列表、CPU使用率、内存占用等信息。
    在Android系统中, 可以通过终端或ADB shell来使用top命令。以下是使用top命令查看系统资源使用情况的示例代码：
    ```bash
    adb shell
    top
    ```
    执行上述代码后, 将显示实时的进程列表、CPU使用率、内存占用等信息。
2. free命令
    - free命令用于查看系统内存的使用情况, 包括总内存、已使用内存、空闲内存、缓存和缓冲区等信息。
    在Android系统中, 可以通过终端或ADB shell来使用free命令。以下是使用free命令查看系统内存使用情况的示例代码：
    ```bash
    adb shell
    free
    ```
    执行上述代码后, 将显示系统的内存使用情况, 包括总内存、已使用内存、空闲内存、缓存和缓冲区等信息。
3. df命令
    - df命令用于查看文件系统的磁盘空间使用情况, 包括总磁盘空间、已用空间、可用空间和挂载点等信息。
    在Android系统中, 可以通过终端或ADB shell来使用df命令。以下是使用df命令查看磁盘空间使用情况的示例代码：
    ```bash
    adb shell
    df
    ```
    执行上述代码后, 将显示文件系统的磁盘空间使用情况, 包括总磁盘空间、已用空间、可用空间和挂载点等信息。
4. 如何使用top、free、df命令查看系统资源使用情况
    - trace命令概述
    trace命令是Android系统中一个非常有用的工具, 可以用来跟踪Android应用程序的运行情况, 包括CPU使用情况、函数调用耗时、线程活动等信息。
    1. trace命令参数含义
    - `-b`: 指定要跟踪的缓冲区, 例如main、radio、events等。
    - `-f`: 将跟踪结果输出到指定文件。
    - `-e`: 指定要跟踪的事件, 可以是函数调用、线程活动等。
    - `-t`: 设置跟踪的时间长度。
2. 如何使用trace命令来跟踪Android应用程序的运行情况
    - 在Android系统中, 可以通过终端或ADB shell来使用trace命令。以下是使用trace命令跟踪应用程序运行情况的示例代码：
    ```bash
    adb shell
    trace -f my_trace_output.trace -e sched freq power cpu
    ```
    上述命令将会跟踪CPU的调度、频率、功耗等信息, 并将结果输出到my_trace_output.trace文件中。
3 跟踪CPU使用情况
    ```bash
    adb shell
    trace -f my_trace_output.trace -e sched freq power cpu
    ```
    上述命令将会跟踪CPU的调度、频率、功耗等信息, 并将结果输出到my_trace_output.trace文件中。
4. 跟踪函数调用耗时
    ```bash
    adb shell
    trace -f my_trace_output.trace -e 'probe process(ProcessName) { printf("%s", thread_indent(1)); printf("%s\n", user_stack()); }'
    ```
    上述命令将会跟踪指定进程的函数调用情况, 并将结果输出到my_trace_output.trace文件中。
5. 跟踪线程活动
    ```bash
    adb shell
    trace -f my_trace_output.trace -e sched_switch sched_wakeup sched_waking sched_blocked_reason sched_cpu_hotplug
    ```
    上述命令将会跟踪线程的切换、唤醒、阻塞等活动, 并将结果输出到my_trace_output.trace文件中。
6. pm 、am
    - am
    pm命令是Android系统中一个强大的工具, 用于管理应用程序的安装、卸载、查询和清理等操作。
    pm命令常用参数含义
    -i：显示应用程序的安装信息, 包括包名、版本号、安装路径等。
    -l：列出已安装应用程序的包名列表。
    -u：卸载指定包名的应用程序。
    -f：显示应用程序的安装路径。
    -s：显示应用程序的安装大小。
    -c：清除指定包名的应用程序的缓存数据。
    - am
    am命令用于与Android应用程序进行交互, 可以启动、停止、调试应用程序, 发送广播等。
    2.1 am命令常用参数含义
    - start：启动一个应用程序。
    - stop：停止一个正在运行的应用程序。
    - broadcast：发送一个广播消息给应用程序。
    - instrument：运行一个应用程序的测试用例。
    - profile：启动应用程序的性能分析。
    3. 如何使用pm、am命令来管理Android设备上的应用程序
    - 在Android系统中, 可以通过终端或ADB shell来使用pm、am命令。以下是使用pm、am命令来管理应用程序的示例代码：
    安装应用程序
    ```bash
    adb install example.apk
    ```
    上述命令将会安装名为example.apk的应用程序到Android设备中。
    卸载应用程序
    ```bash
    adb uninstall com.example.app
    ```
    上述命令将会卸载包名为com.example.app的应用程序。
    启动应用程序
    ```bash
    adb shell am start -n com.example.app/.MainActivity
    ```
    上述命令将会启动包名为com.example.app, 主Activity为MainActivity的应用程序。
    停止应用程序
    ```bash
    adb shell am force-stop com.example.app
    ```
    上述命令将会停止运行包名为com.example.app的应用程序。
    getprop、setprop
    getprop和setprop是Android系统中的两个命令, 用于获取和设置系统属性。
    1. getprop命令
    ```bash
    adb shell getprop [property_name]
    ```
    property_name是要获取的系统属性的名称。
    例如, 如果要获取Android设备的型号信息, 可以使用以下命令：
    ```bash
    adb shell getprop ro.product.model
    ```
    2. setprop命令
    ```bash
    adb shell setprop [property_name] [property_value]
    ```
    property_name是要设置的系统属性的名称。
    property_value是要设置的系统属性的值。
    请注意, 使用setprop命令可能需要root权限。
    例如, 如果要将Android设备的屏幕密度设置为240dpi, 可以使用以下命令：
    ```bash
    adb shell setprop ro.sf.lcd_density 240
    ```
    请注意, 在修改系统属性时, 谨慎操作, 确保了解具体的属性名称和取值范围, 避免对系统造成不可逆的影响。
综上所述, getprop和setprop命令是在Android系统中用于获取和设置系统属性的工具。通过它们, 您可以查看和修改一些与设备和系统相关的属性信息。

### settings命令
settings命令用于在Android设备上访问和修改系统设置。您可以使用adb shell settings命令来执行各种操作。以下是settings命令的一些常见用法：
1. 获取设置值
    ```bash
    adb shell settings get setting_name
    ```
    其中, setting_name是要获取的设置名称。例如, 要获取屏幕亮度设置的值, 可以使用以下命令：
    ```bash
    adb shell settings get system screen_brightness
    ```
2. 修改设置值
    ```bash
    adb shell settings put setting_namespace setting_name value
    ```
    其中, setting_namespace是设置所属的命名空间, setting_name是要修改的设置名称, value是要设置的新值。例如, 要将屏幕亮度设置为255, 可以使用以下命令：
    ```bash
    adb shell settings put system screen_brightness 255
    ```
3. 列出所有设置项
    ```bash
    adb shell settings list
    ```
    该命令将会列出所有可用的设置项及其名称。
综上所述, settings命令提供了在Android设备上访问和修改系统设置的功能。通过适当使用这些命令, 您可以获取和修改各种设置项的值, 以满足您的需求。
