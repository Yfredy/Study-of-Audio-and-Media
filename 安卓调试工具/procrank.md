# procrank
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
