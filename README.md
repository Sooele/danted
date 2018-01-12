<h2>Danted Socks5 一键安装脚本</h2>
<h3>******安装选项</h3>

| 选项 | 描述 |
| ----- | ----- |
| --port= | socks5 端口号码 |
| --ip=;; | 配置的IP地址，默认全部开启，使用;分格 |
| --user= | pam认证用户名 |
| --passwd= | pam认证用户密码|
| --master= | 免认证地址，例如 github.com 或者 8.8.8.8/32 |
    
<h3>******功能特点</h3>
<ul>
<li>1. 采用dante稳定版本 1.3.2 编译安装。</li>
<li>2. 自动识别系统IP（默认排除192.168.0.*， 10.0.0.*,127.0.0.*）,根据安装命令选择部分Ip或者全部IP安装(多IP环境)。</li>
<li>3. 采用PAM 用户认证，认证不需要添加系统用户（默认添加进程用户sock），删除、添加用户方便，安全。</li>
<li>4. sock5 运行状态查看,系统启动后自动加载。</li>
<li>5. <b>完美支持多访问进出口（多IP的环境，支持 使用IP-1，访问网站IP查询为IP-1）。</b></li>
<li>6. 认证方式可选： 无用户名密码，系统用户名密码，Pam用户名密码</li>
<li>7. 完美支持Centos/Debian,自动识别系统进行安装配置。[注意，经反馈，Centos 5 无法使用。]</li>
<li>8. 自定义对连接客户端认证方式，支持白名单即支持某些IP/IP段无需认证即可连接。</li>
</ul>
<h3>******已解决问题</h3>
<ul>
<li>测试64位系统 centos 会出现认证失败 请添加一条命令 <code>cp /lib/security/pam_pwdfile.so /lib64/security/ </code></li>
<li><code>
/etc/danted/sbin/sockd: /lib/x86_64-linux-gnu/libc.so.6: version `GLIBC_2.14' not found (required by /etc/danted/sbin/sockd)
</code>
</li>
</ul>
<h3>******未解决问题</h3>
<ul>
<li>1. 分析log对连接sock5的用户进行统计。</li>
</ul>
<hr>
<h3>******安装用说明</h3>
<ul>
<li> 1. 下载 
<code> wget --no-check-certificate https://raw.github.com/Sooele/danted/master/install.sh -O install.sh </code> </li>
<li> 2. [可选] 修改 默认参数，DEFAULT_PORT 为默认端口，DEFAULT_USER PAM用户名，DEFAULT_PAWD PAM用户对应密码 MASTER_IP 为免认证白名单（域名，IP可选：  如默认的buyvm.info 或者具体Ip 8.8.8.8/32 ）</li>
<li> 3. 修改后，执行(不懂的，直接用下面的格式，自己修改) <code> bash install.sh </code> </li>
<li> 3. 修改后，执行<code>bash install.sh --ip="server_ip" --port=xxx --user=xxxx --passwd=xxxx</code></li>
<li> 4. 若运行结束后显示 Dante Server Install Successfuly! 则表明成功。
<p>显示 Dante Server Install Failed! 则表明安装失败，求留言反馈操作系统+具体问题。</p></li>
</ul>
******安装后使用说明
## Management

| command | option | description |
| :--- | :--- | --- |
| service sockd start | /etc/init.d/sockd start | 启动socks5服务器守护进程 |
| service sockd stop | /etc/init.d/sockd stop | 停止socks5服务器守护进程 |
| service sockd restart | /etc/init.d/sockd restart | 重新启动socks5服务器守护进程 |
| service sockd reload | /etc/init.d/sockd reload | 重新加载socks5服务器守护进程 |
| service sockd status | | 系统进程状态 |
| service sockd state | /etc/init.d/sockd state | 运行状态 |
| service sockd tail | /etc/init.d/sockd tail | sock 日志 |
| service sockd adduser | /etc/init.d/sockd adduser | 添加pam-auth用户：service sockd adduser NAME PASSWORD |
| service sockd deluser | /etc/init.d/sockd deluser | 删除pam-auth用户：service sockd deluser NAME |

## <h></a>通过测试Vultr <a href="https://www.vultr.com/?ref=7205255">https://www.vultr.com/</a></h2>
| OS release | Platform | Provider | Result |
| :--- | :--- | --- |  --- | 
| Debian GNU/Linux 8 (jessie) | x86_64 | vultr | 通过|
| Debian GNU/Linux 7 (wheezy) | x86_64 | vultr | 通过 |
| Debian GNU/Linux 7 (wheezy) | i686 | vultr | 通过 |
| Ubuntu 16.10 (Yakkety Yak)  | x86_64 | vultr | 通过 |
| Ubuntu 14.04.5 LTS | i686 | vultr | 通过
| CentOS Linux 7 (Core) | x86_64 | vultr | 通过 |
| CentOS Linux 6 | x86_64 | vultr | 通过 |
| CentOS Linux 6 | i686 | vultr | 通过 |



<h3>******使用注意事项</h3>
<ul>
<li> 1. 绝大部分浏览器（除了Opera）都不支持带密码认证的Socks5，所以使用电脑需要安装proxifier/proxycap 等软件做验证处理。</li> 
<li> 2. 如果是固定IP/Ip 段 可以修改配置文件，设置白名单访问。</li>
<ol>
<li>进入 /etc/danted/ 找到配置文件</li>
<li>修改 第一个pass {} 模块下的 from: Master_IP/32 to: 0.0.0.0/0 . 把 Master_IP/32 修改为需要使用代理的Ip段/IP地址 如 114.114.114.0/24 或者 5.5.5.5/32 . 多个访问源，请复制多个 client pass {} 模块</li>
<li>重启Danted 进程 service danted restart </li>


# Sockd
**Dante socks5 server (v1.3.2) auto-install and management script** 

## About
To build a socks5 server, we have lots of open-source programs to reach that, [Dante](https://www.inet.no/dante/) is one of them.
I have been using Dante for years and starting to write this auto-install and management script two years ago.
This is the second update to match the systemd and new OS release like Debian 8 , CentOS 7.

Comparing with the apt-get or building from source manually, this script will benefit you bellow

* Auto-recognize, detect the machine's system automatically and compile from source code.
* Auto-config, check the system's network or read from argument to auto-generate config file.
* Same-rotation, in multi-ipaddr system. It works like when using different ip address to connect socks5, your external ip address will be different. That's the main reason why I using Dante for years.
* Multi-authorization, you can configure authorization by pam, system or using whitelist.

## Install

```bash
wget --no-check-certificate https://raw.github.com/Sooele/danted/master/install.sh -O install.sh 
bash install.sh

# run with options: bash install.sh option1 option2
bash install.sh --ip="A.A.A.A:B.B.B.B" --port=2016 --user=sockd --passwd=sockd --whitelist="X.X.X.X/32"

```

* *if you want to uninstall, using this command*

```bash
bash install.sh --uninstall
```
```
bash install.sh --ip="server_ip" --port=xxx --user=xxxx --passwd=xxxx
```

* *if you want to add user*

```bash
/etc/init.d/sockd adduser USERNAME PASSWORD
```

## Options

| Long Option | Short Option | Value refer | description |
| :--- | :--- | --- | --- |
| --ip=                | | ip address list (a.a.a.a:b.b.b.b) *#change ';' to ':' * | Socks5 Server Ip address |
|  --port=             | | Default: 2016| port for dante socks5 server |
| --user=              | | Pam-Auth Username | Socks5 Auth user |
| --passwd=            | | Pam-Auth Password |Socks5 Auth passwd |
| --whitelist=         | | whitelist ip range (a.a.a.a/32:b.b.b.b/32) |Socks5 Auth IP list |
| --whitelist-url=     | | online white list file (url) | Socks Auth whitelist http online |
| --from-package       | -p    | --    | Install package from Bin package |
| --update-whitelist   | -u    | --    |  update white list |
| --force              | -f    | --    | force install sockd |
| --help               | -h    | --    | print help info |

## Management

| command | option | description |
| :--- | :--- | --- |
| service sockd start | /etc/init.d/sockd start | start socks5 server daemon |
| service sockd stop | /etc/init.d/sockd stop | stop socks5 server daemon |
| service sockd restart | /etc/init.d/sockd restart | restart socks5 server daemon |
| service sockd reload | /etc/init.d/sockd reload | reload socks5 server daemon |
| service sockd status | | systemd process status |
| service sockd state | /etc/init.d/sockd state | running state |
| service sockd tail | /etc/init.d/sockd tail | sock log tail |
| service sockd adduser | /etc/init.d/sockd adduser | add pam-auth user:  service sockd adduser NAME PASSWORD |
| service sockd deluser | /etc/init.d/sockd deluser | delete pam-auth user:  service sockd deluser NAME |


## Test Pass https://www.vultr.com/?ref=7205255


| OS release | Platform | Provider | Result |
| :--- | :--- | --- |  --- | 
| Debian GNU/Linux 8 (jessie) | x86_64 | vultr | pass |
| Debian GNU/Linux 7 (wheezy) | x86_64 | vultr | pass |
| Debian GNU/Linux 7 (wheezy) | i686 | vultr | pass |
| Ubuntu 16.10 (Yakkety Yak)  | x86_64 | vultr | pass |
| Ubuntu 14.04.5 LTS | i686 | vultr | pass
| CentOS Linux 7 (Core) | x86_64 | vultr | pass |
| CentOS Linux 6 | x86_64 | vultr | pass |
| CentOS Linux 6 | i686 | vultr | pass |


