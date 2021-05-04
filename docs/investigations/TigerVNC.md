# TigerVNC 仓库结构

    ├── cmake
    ├── common  Unix和Windows公共文件
    ├── contrib
    ├── doc
    ├── java  Java版本
    ├── media  图标等UI资源
    ├── po	多语言翻译相关
    ├── release
    ├── tests
    ├── unix  Unix的Server Stable
    ├── vncviewer  VNC client
    └── win	Windows的Server BUGGY

## VNCviewer
    ├── BaseTouchHandler.cxx
    ├── BaseTouchHandler.h
    ├── CConn.cxx
    ├── CConn.h
    ├── CMakeLists.txt
    ├── DesktopWindow.cxx
    ├── DesktopWindow.h
    ├── EmulateMB.cxx
    ├── EmulateMB.h
    ├── GestureEvent.h
    ├── GestureHandler.cxx
    ├── GestureHandler.h
    ├── OptionsDialog.cxx
    ├── OptionsDialog.h
    ├── PlatformPixelBuffer.cxx
    ├── PlatformPixelBuffer.h
    ├── ServerDialog.cxx
    ├── ServerDialog.h
    ├── Surface.cxx
    ├── Surface.h
    ├── Surface_OSX.cxx
    ├── Surface_Win32.cxx
    ├── Surface_X11.cxx
    ├── UserDialog.cxx
    ├── UserDialog.h
    ├── Viewport.cxx
    ├── Viewport.h
    ├── Win32TouchHandler.cxx
    ├── Win32TouchHandler.h
    ├── XInputTouchHandler.cxx
    ├── XInputTouchHandler.h
    ├── cocoa.h
    ├── cocoa.mm
    ├── fltk_layout.h
    ├── gettext.h
    ├── i18n.h
    ├── keysym2ucs.c
    ├── keysym2ucs.h
    ├── menukey.cxx
    ├── menukey.h
    ├── osx_to_qnum.c
    ├── parameters.cxx
    ├── parameters.h
    ├── resource.h
    ├── touch.cxx
    ├── touch.h
    ├── vncviewer.cxx	main，包括命令行参数处理, 启动流程, 错误报告等, 但不涉及实现细节
    ├── vncviewer.desktop.in.in
    ├── vncviewer.h
    ├── vncviewer.man
    ├── vncviewer.rc.in
    ├── win32.c
    ├── win32.h
    └── xkb_to_qnum.c

## Xserver
    ├── .gitignore
    ├── Input.c  # 与鼠标, 键盘的设备初始化, 信息读取有关
    ├── Input.h
    ├── InputXKB.c  # 利用X11进行keyboard输入处理
    ├── Makefile.am
    ├── RFBGlue.cc  # (!重要)包含VNC对RFB的初始化, 配置, 参数获取, 日志生成等, 且采用TCPSocket, 包含根据fd找到Socket端口, 检测端口使用情况等功能
    ├── RFBGlue.h
    ├── RandrGlue.c  # 涉及桌面窗口的大小改变, 旋转, 镜像等操作
    ├── XorgGlue.c  # 获取屏幕数量/格式/长宽等函数 
    ├── XorgGlue.h
    ├── XserverDesktop.cc  # (!重要)利用common里network/rfb定义的函数和拓展等功能, 统筹用户连接, 鼠标更新, Socket侦听, 阻塞/非阻塞更新等
    ├── XserverDesktop.h
    ├── Xvnc.man  # Xtigervnc的帮助手册
    ├── buildtime.c  # build时间记录
    ├── qnum_to_xorgevdev.c  # 各个按键到xorgdev自定义序号的映射
    ├── qnum_to_xorgkbd.c  # 各个按键到xorgkbd自定义序号的映射
    ├── vncBlockHandler.c  # vncFdEntry结构体封装了fd, read/write等属性
    ├── vncBlockHandler.h
    ├── vncExt.c  # 与vncExtInit有关，具体作用不详
    ├── vncExtInit.cc  # (!重要)VNC拓展管理, 包括RFB协议的参数设置, 像素格式获取, 剪切板操作, 多屏的Tcp连接建立并形成多个XserverDesktop, 处理socket事件, 客户端连接请求的允许/断开等 
    ├── vncExtInit.h
    ├── vncHooks.c  # 桌面图像获取
    ├── vncHooks.h
    ├── vncModule.c  # module初始化涉及RFB初始化， 拓展初始化等， 具体作用不详
    ├── vncSelection.c  # 处理剪切板的权限请求和数据等
    ├── vncSelection.h
    ├── xorg-version.h  # 确定X.Org版本的宏
    └── xvnc.c  # 定义屏幕信息, 图像编码顺序等与VFB(virtual frame buffer)相关结构和函数,以及RandR(resize, rotate and reverse)的模式设置等

## Other Resources

RFB git：https://github.com/rfbproto/rfbproto

VNC和RFB protocol(翻译)：https://blog.csdn.net/forever_feng/article/details/4703088?utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-2.control&dist_request_id=1330144.22741.16181253332079191&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-2.control

