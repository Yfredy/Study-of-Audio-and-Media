# top、free、df
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