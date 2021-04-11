# 目前开源远程控制软件/协议调研 #

> 协议均为端到端的协议, Server指主动共享桌面的端

1. **Remmina**: **Client**

    一款支持RDP, SSH, VNC, NX, SPICE的**客户端**GUI工具

2. **VNC (Virtual Network Console)**: 相当于一款协议

    - 截图, 压缩, 传输, [较为低效](https://superuser.com/questions/285250/why-is-vnc-on-windows-so-slow)
    - 代表软件: 
      - [TigerVNC](https://tigervnc.org/): **Client&Server**
        开源, 跨平台, 未试用
      - [gnome-remote-desktop](https://wiki.gnome.org/Projects/Mutter/RemoteDesktop): **Server**
        开源, 已跨平台试用, 有可感受的延迟(约300ms级)
    
3. **RDP (Remote Desktop Protocol)**: 微软的远程桌面协议

    - 针对远程控制做了桌面系统级的优化: 对窗口, 指针的检测等
    - 代表软件:
      - [xrdp](http://xrdp.org/): **Server**
        RDP for X
        开源, 未成功试用, 似乎是不太能支持Gnome
      - Windows远程控制: **Client&Server**
        RDP的发源, 闭源

4. **NX**: NoMachine公司的远程桌面协议

    - 基于SSH, 快速
    - 代表软件:
      - [FreeNX](https://sourceforge.net/projects/freenx.berlios/): **Client&Server**
        2008年发布的开源版本, 随后转入闭源, FreeNX不再更新
      - [nomachine](https://www.nomachine.com/): **Client&Server**
        闭源版本, 已跨平台试用, 延时极低, 约50ms级
    
5. **x2go**: FreeNX的新替代品 (**Client&Server**)

    - 基于SSH
    - 有Windows的**Client**, 但**Server**只支持Linux
    - 开源, 未试用

6. **xpra**: 远程控制软件 (**Client&Server**)

    - 可用SSL, SSH, WS等多种协议
    - 开源, 跨平台, 未试用



## RDP details:

相关链接：
http://www.voidcn.com/article/p-syoebouy-bdx.html
https://docs.microsoft.com/zh-CN/troubleshoot/windows-server/remote/understanding-remote-desktop-protocol
https://blog.csdn.net/qq_38526635/article/details/81672490

http://www.doc88.com/p-478332300292.htmlhttp://www.doc88.com/p-478332300292.html

Remote Desktop Protocol是一个庞大的协议集合体。比方说包含了基本连接和远程图形处理协议、多点通讯服务协议、模式传输服务协议、Microsoft点对点压缩（MPPC）协议、Netlogon远程协议、远程过程调用协议、终端服务网关服务器协议、多媒体会议网络特定数据协议以及远程桌面网关服务器协议等等的协议集。这些协议经过组合、调用以及集成，完美的展现出用户终端计算机系统和远程计算机系统之间的系统交互。

![image-20210406234951959](C:\Users\Victor\AppData\Roaming\Typora\typora-user-images\image-20210406234951959.png)

|            |                                                              |
| ---------- | ------------------------------------------------------------ |
| 网络连接层 | RDP协议建立在TCP/IP协议之上，由于传输的数据量比较大，因此在协议的底层首先定义一层网络连接层。它定义了一个完整的RDP数据逻辑包，以避免由于网络包长度过长而被分割使数据丢失。 |
| ISO数据层  | 在网络连接层之上是ISO数据层，它表示RDP数据的正常连接通信。   |
| 虚拟通道层 | 在ISO数据层之上，RDP协议定义一个虚拟通道层，用以拆分标示不同虚拟通道的数据，加快客户端处理速度，节省占用网络接口的时间。 |
| 加密解密层 | 在虚拟通道层之上，RDP定义一个数据加密解密层。此层用于对所有的功能数据进行加密、解密处理。 |
| 功能数据层 | 在加密解密层之上是功能数据，画面信息，本地资源转换，声音数据，打印数据等所有的功能数据信息都在此层进行处理。另外，根据数据类型的不同，这些数据都有各自不同层次的分割，他们的内部层次结构将在各个功能模块中进行阐述。 |

RDP 堆栈实例中值得讨论的四个组件是：

- MCSMUX (多点通信)
- GCC 会议 (通用会议)
- Wdtshare.sys
- Tdtcp.sys

MCSmux 和 GCC 是 T.120 系列中 () 的一部分。 MCS 由两个标准决定：

- T.122：它定义多点服务
- T.125：它指定数据传输协议

MCSMux 控件：

- 通过将数据多路复用到协议内的预定义虚拟通道进行通道分配
- 优先级
- 要发送的数据的分段

实质上，它从 GCC 的角度将多个 RDP 堆栈抽象为一个实体。 GCC 负责管理这些多个渠道。 GCC 允许创建和删除会话连接，并控制 MCS 提供的资源。 目前， (每个终端服务器协议，仅支持 RDP 和 Citrix 的 ICA) 在侦听器堆栈中加载协议堆栈 (等待连接请求) 。 终端服务器设备驱动程序协调和管理 RDP 协议活动。 它由较小的组件组成：

- RDP 驱动程序 (Wdtshare.sys) UI 传输、压缩、加密、帧等。
- **传输驱动程序 (Tdtcp.sys) 将协议打包到基础网络协议 TCP/IP。**

RDP 被开发为完全独立于其基础传输堆栈，在此例中为 TCP/IP。 这意味着，我们可以在客户需求增长时为其他网络协议添加其他传输驱动程序，对协议的基础部分进行很少或没有任何重大更改。 它们是网络上 RDP 的性能和扩展性的关键元素。