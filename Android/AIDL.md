# AIDL

AIDL（Android Interface Definition Language）是一种 IDL 语言，用于生成可以在 Android 设备上两个进程之间进行进程间通信（IPC）的代码。 通过 AIDL，可以在一个进程中获取另一个进程的数据和调用其暴露出来的方法，从而满足进程间通信的需求。通常，暴露方法给其他应用进行调用的应用称为服务端，调用其他应用的方法的应用称为客户端，客户端通过绑定服务端的 Service 来进行交互。

## 创建 AIDL 文件
AIDL 文件可以分为两类。一类用来声明实现了 Parcelable 接口的数据类型，以供其他 AIDL 文件使用那些非默认支持的数据类型。还有一类是用来定义接口方法，声明要暴露哪些接口给客户端调用。在 AIDL 文件中需要明确标明引用到的数据类型所在的包名，即使两个文件处在同个包名下。

默认情况下，AIDL 支持下列数据类型：

八种基本数据类型：`byte、char、short、int、long、float、double、boolean、String，CharSequence、List`类型。
`List`承载的数据必须是AIDL支持的类型，或者是其它声明的AIDL对象
`Map`类型。Map承载的数据必须是AIDL支持的类型，或者是其它声明的AIDL对象
客户端和服务端都需要创建，我们先在服务端中创建，然后复制到客户端即可。在 Android Studio 中右键点击新建一个 AIDL 文件。