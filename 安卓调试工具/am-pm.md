# pm 、am
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
