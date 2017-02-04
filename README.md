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
dns-nameservers 192.168.0.254 114.114.114.114`

关闭 dhcp
`systemctl stop dhcpcd`
`systemctl disable dhcpcd`
`systemctl daemon-reload`

## 2 Configure apache and php and mysql
`# apt-get install apache2 php5 mysql-server`

