### 锁屏后播放软件会自动暂定

[参考帮助](https://answers.microsoft.com/zh-hans/windows/forum/windows_10-performance/win10%E9%94%81%E5%AE%9A%E5%B1%8F%E5%B9%95%E5%90%8E/50f37c31-c1c7-419e-bbec-693935e8ac35), 执行命令: `powercfg -h off`

### 查看端口占用情况

`netstat -ano | find "xxx"`

## PsList 工具
[下载地址](https://docs.microsoft.com/zh-cn/sysinternals/downloads/pslist)

PsList 工具包包含了一系列查询进程和线程的工具.

### pslist

查看某个进程中的线程详情: `pslist -dmx xxx[taskID]`