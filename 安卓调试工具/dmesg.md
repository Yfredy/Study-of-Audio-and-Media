# dmesg

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