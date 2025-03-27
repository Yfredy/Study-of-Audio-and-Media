# adb调试

ADB(Android Debug Bridge)是一个通用命令行工具, 可让你与模拟器实例或连接的 Android 设备进行通信。以下是详细的 ADB 调试教程：

## 1. 安装 ADB
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

## 2. 启用设备的 USB 调试模式
- **安卓设备**
    - 打开设备的“设置”应用。
    - 找到“关于手机”或“关于设备”选项。
    - 连续点击“版本号”7 次, 开启开发者选项。
    - 返回“设置”主界面, 进入“开发者选项”, 开启“USB 调试”。
- **安卓模拟器**：大多数安卓模拟器默认开启了 USB 调试模式, 无需额外设置。

## 3. 连接设备
- 使用 USB 数据线将安卓设备连接到电脑。
- 打开终端或命令提示符, 输入 `adb devices` 命令。如果设备连接成功且 USB 调试已开启, 你将看到设备的序列号以及设备状态为 `device`, 例如：
    ```plaintext
    List of devices attached
    0123456789ABCDEF    device
    ```

## 4. 常用 ADB 命令
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

## 5. 断开连接
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
