# raspbian Initial Install
raspberry PI debian linux v8
# After install image
## 1 Configure Network
首先安装必要的软件

`# apt-get install vim tree`

` # vim /etc/network/interface` 
`auto eth0
iface eth0 inet static
address 192.168.0.6
netmask 255.255.255.0
network 192.168.0.0
gateway 192.168.0.254
dns-nameservers 192.168.0.254 114.114.114.114
`

关闭 dhcp
`systemctl stop dhcpcd`
`systemctl disable dhcpcd`
`systemctl daemon-reload`

## 2 Configure apache and php and mysql
`# apt-get install apache2 php5 mysql-server`


## 3 apr-scan 使用
如果没有这个软件包，则 apt-get install nmap arp-scan 安装之
命令示例：
`# arp-scan --interface=eth0 --localnet --ouifile=/usr/share/ieee-oui.txt`
其中　ieee-oui.txt 可以从网上下载最新版本的MAC 与厂商的对照表， 详细信息请参阅：https://regauth.standards.ieee.org/standards-ra-web/pub/view.html ，下载回来后略加工就可以形成 ieee-oui.txt 文件格式。其中第一列为MAC硬件地址的前4个字节，第二个字段为制造商，中间空格\t分隔

# 配置局域网 SAMBA我的配置文件如下： 
`[global] 
server string = Raspberry PI 1
# guest ok = yes 
security = user 
registry shares = yes 
syslog = 0 
map to guest = bad user 
workgroup = WORKGROUP 
bind interfaces only = No 
encrypt passwords = true 
log level = 0 
unix extensions = No 
wide links = yes 
unix charset = UTF-8 
dos charset = cp936 
printable = no

[media]    
path = /media/stick    
comment = P1 Media Center    
valid users = pi spender @users    
force group = users    
create mask = 0644    
directory mask = 0744        
locking = no    
writable = yes        
printable = no    
write list = spender pi

[system-logs]    
path = /var/log    
guest ok = yes    
read only = yes    
force user = root    
browseable = yes
`
修改完成以后，使用命令 `testparm` 检测一下是否参数使用正确。 `/etc/init.d/samba restart` 重新启动服务就可以看见了
用命令： `smbpasswd spender` 设置三个用户的访问密码
`gdedit -w -L` 查看当前所有用户

# 配置 minildna 有点遗憾的是，它不支持 中文文件名

