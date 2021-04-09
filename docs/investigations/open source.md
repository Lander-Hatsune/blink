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

