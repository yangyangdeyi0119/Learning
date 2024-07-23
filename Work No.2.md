# Work No.2

### 一、了解代码结构

**KL_440XX_KLIPPER**

- app-server
  - 创想云app的服务端
- audio-server
  - 音频的服务端，没有启用，搁置
- bin
  - 编译文件存放地
- burn-server
  - 烧录设置
- display-server
  - 显示屏的代码库
  - lvg7.11  旧版本，已经搁置
  - lvg8.0  主要版本
- doc
  - 代码解释，readme文件存放
- global
  - 底层库文件存放区
- master-server
  - 主要操作代码存放区
  - APP
    - 与app-server对接的管理文件
  - Appointment
  - Audio
    - 与audio-server对接的管理文件
  - Base
  - Burn
    - 与burn-server对接的管理文件
  - Control
    - 主要的打印机控制程序
  - Display
    - 与display-server对接的管理文件
  - out
    - 各类编译输出文件存放地
  - SysTransfer
  - Upgrade
    - 升级文件
  - UserMain
    - 主程序存放，主要用来调用函数
  - Web
    - 与web-server对接的管理文件
  - Wifi
    - 与wifi-server对接的管理文件
- monitor
  - 监控程序
- upgrade-server
  - 系统升级程序存放
- web-server
  - 局域网服务端，用于类似创想云与机器链接
- wifi-server
  - WiFi服务端用于本地TCP协议链接等等

### 二、代码常见英文

extruder：喷嘴

heaterBed：热床

Material：耗材

Execute：执行

请求消息：REQ

响应消息：RES

### 三、知识点总结

- atoi(doubleSpeed + strlen("M220 S"));
  - 功能：把字符串转换成整型数。

- strstr(readBuff, "M220 S");
  - strstr函数是在一个字符串中查找另一个字符串的第一次出现，并返回该位置的指针，如果找不到，则返回NULL。
- memcpy(ringBuff.cmd, readBuff, strlen(readBuff));
  - C 库函数 **void \*memcpy(void \*str1, const void \*str2, size_t n)** 从存储区 **str2** 复制 **n** 个字节到存储区 **str1**。

- memset(&ringqp->array[ringqp->tail], 0, sizeof(Ring_t));
  - C 库函数 **void \*memset(void \*str, int c, size_t n)** 用于将一段内存区域设置为指定的值。
  - memset() 函数将指定的值 c 复制到 str 所指向的内存区域的前 n 个字节中，这可以用于将内存块清零或设置为特定值。在一些情况下，需要快速初始化大块内存为零或者特定值，memset() 可以提供高效的实现。在清空内存区域或者为内存区域赋值时，memset() 是一个常用的工具函数。
- void SetAutoPrintInfo(PrintFileInfo_t info) { printInfo = info; }
  - 这段代码的作用是将传入的 PrintFileInfo_t类型的参数 info赋值给全局变量或静态变量 printInfo
  - 数据结构和函数的综合作用是为打印任务提供一个全面的管理和控制机制。它们不仅仅是初始变量的定义，还包括更新、存储和管理打印任务信息的功能。
-  fseek(fd, 0, SEEK_SET);
  - C 库函数 **int fseek(FILE \*stream, long int offset, int whence)** 设置流 **stream** 的文件位置为给定的偏移 **offset**，参数 offset 意味着从给定的 **whence** 位置查找的字节数。
- CREATE_MESSAGE_PACKAGE(send, size, MSG_ORIGIN_CONTROLLER, MANAGER_CMD_GCODE_SET_NOZZLE_TEMP_ANS, buff, len);
  - 创建响应信息包
  - 将消息的来源设置为MSG_ORIGIN_CONTROLLER
  - 将消息的类型设置为MANAGER_CMD_GCODE_SET_MAX_ACCELERATION_ANS，表示这是一个响应“设置最大加速度”命令的消息
  - 将缓冲区buff中的数据以及数据的长度len设置为消息的数据内容，将消息的大小（包括头部和数据部分）设置为size1。
- MANAGER_MSG_SEND(cmd.origin, &send, size);
  - 将打包好的消息发送回给调用者，通知其设置数据的结果。
- AddGcodeListCmd(CXSW_GET_LEVEL_POINTS_NUM, 0, &tCmd, MSG_ORIGIN_CONTROLLER);
  - 这个函数里面包含了发送指令，是使用串口发送，已经弃用
- AddKlipperCmd("gcode/script", params, SET_MAX_SPEED_NUM, head->origin);
  - 这个函数是使用socket发送
- strcmp()字符串比较函数
  - int strcmp(const char *str1, const char *str2)
  - **str1** -- 要进行比较的第一个字符串。**str2** -- 要进行比较的第二个字符串。
- gettimeofday()返回当前时间
- PopenSystem()用于终端执行指令