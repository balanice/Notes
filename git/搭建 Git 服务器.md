# git 搭建本地仓库

## 服务器操作

1. 创建名称为 git 的用户, 用来运行 git 服务: 
    ```shell 
    sudo adduser git 
    ``` 

2. 收集用户的公钥, 也就是他们自己的 **id_rsa.pub** 文件中的内容, 把这些内容导入服务器 **/home/git/.ssh/authorized_keys** 文件里, 一行一个. 

3. 初始化 git 仓库 
    ```shell 
    git init --bare sample.git 
    ``` 
    Git 就会创建一个裸仓库, 裸仓库没有工作区, 因为服务器上的 git 仓库纯粹是为了共享, 所以不让用户直接登陆到服务器上去改工作区, 并且服务器上的 git 仓库都会以 `.git` 结尾. 然后, 把 owner 改为 git: 
    ```shell 
    sudo chown -R git:git sample.git 
    ```

4. 禁用 shell 登陆 git. 出于安全考虑, 创建的 git 用户不允许登陆 shell, 这可以通过编辑 `/etc/passwd` 文件完成. 找到类似下面一行: 
    ```shell 
    git:x:1001:1001:,,,:/home/git:/bin/bash 
    ``` 
    改为: 
    ```shell 
    git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell 
    ``` 
    这样, git 用户可以正常通过 ssh 使用 git 服务, 但无法登陆 shell. 

5. 设置 git 用户有效期. 部分 Linux 系统默认新建用户的密码有效期为90天, 可以用如下命令查看 git 用户密码有效期: 
    ```shell 
    sudo chage -l git 
    ``` 

    如果 git 用户有效期不为永久有效, 可以通过如下命令设置为永久有效: 
    
    ```shell 
    sudo chage -M 99999 git 
    ``` 

6. 修改 ssh 默认端口号. 部分公司为了安全会禁用端口号小于8000的端口的对外访问权限, 这个时候就要手动设置 ssh 的默认端口了. 首先使用如下命令查看 ssh 端口号: 

    ```shell 
    sudo netstat -tnlp | grep ssh 
    ``` 
    如果 ssh 端口号为默认的22, 那么就需要进行修改了. 使用 **vim /etc/ssh/sshd_config** 修改 **Port 22** 为 **Port 8001** 之类大于 8000 的端口, 然后使用如下命令重启 ssh 服务: 
    ```shell 
    sudo service ssh restart 
    ``` 
    再使用查看端口号的命令就可以看到 ssh 端口号已经修改为刚刚设置的了;"

## 客户端操作

 1. 安装 git 
 2. 配置 git 用户名及邮箱, 先使用如下命令查看是否已设置了用户名及邮箱: 
    ```shell 
    git config --list 
    ``` 
     查看 user.name, user.email 配置是否正确, 如果不正确, 则通过如下命令进行配置: 
    ```shell 
    git config --global user.name "username" 
    git config --global user.email "user@email.com"
    ``` 
 3. 使用如下命令生成公钥: 
  
     ```shell 
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com" 
     ``` 

     一路 Enter 即可,生成的公钥在 Linux 系统下的 **/home/xxx/.ssh/** 目录中, Windows 系统在 **C:\\Users\\xxx\\.ssh** 目录中, xxx 为电脑用户名 
 4. 将生成的公钥提供给服务器管理员来添加权限; 
 5. 从服务器克隆代码: 
      
     ```shell 
     git clone git@server:/srv/sample.git 
     ``` 
  
     server 为服务器地址 
 6. 服务器修改 ssh 默认端口后 git 配置服务器有时候会在某些情况下修改默认的 ssh 端口号, 这个时候 git 使用原来的方法就不能访问了, 这个时候就需要进行一定的修改. 
  
     * 直接在地址后面加上修改后的端口号, 如 8001, `git clone git@server:8001/srv/sample.git`; 
     * 创建配置文件, 在 Windows 的 **C:\\Users\\username\\\.ssh** 目录或者 Linux 的 **/home/username/.ssh/** 目录下新建  config 文件, **注意, 这个文件没有扩展名**, 在文件中添加如下内容: 
     ```shell 
     host 127.0.0.1    #此处只为示例, 在这里填上服务器地址 
     port 8001 
     ```
