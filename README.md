correr host apd en ubuntu
para el fucking networking de react >:/
Tplink WN7200ND
```
 apt-get install libnl-genl-3-dev libssl-dev libnl-3-dev
 ```
 instalar hostapd de :
http://w1.fi/releases/
y compilar el 2.6

 locate hostapd


buscar la linea y descomentar `CONFIG_LIBNL32=y`
```bash
# Use libnl v2.0 (or 3.0) libraries.
#CONFIG_LIBNL20=y

# Use libnl 3.2 libraries (if this is selected, CONFIG_LIBNL20 is ignored)
CONFIG_LIBNL32=y
```
y make



luego en con el comando `ip addr`:
```bash
7: wlxc46e1f181d5f: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether c4:6e:1f:18:1d:5f brd ff:ff:ff:ff:ff:ff
    inet 192.168.1.67/24 brd 192.168.1.255 scope global dynamic wlxc46e1f181d5f
       valid_lft 86380sec preferred_lft 86380sec
    inet6 fe80::93ed:a710:838c:d86a/64 scope link 
       valid_lft forever preferred_lft forever
```

despues de correr el airmon:
```bash
8: wlan0mon: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ieee802.11/radiotap c4:6e:1f:18:1d:5f brd ff:ff:ff:ff:ff:ff
```

```bash
 cp -R hostapd-2.6 /etc/opt
 sudo cp -R hostapd-2.6 /etc/opt
 cd /etc/opt
 ls
 cd hostapd-2.6/
 ls
 cd hostapd/
 cp defconfig .config
 sudo cp defconfig .config
 nano .config
 sudo nano .config
 make
 sudo make
 sudo make install
 ip addr
 airmon
 sudo apt-get install airmon
 sudo apt-get install aircrack-ng
 airmon-ng
 sudo airmon-ng start wlxc46e1f181d5f
 ip addr
 sudo nano hostapd.conf
 sudo st hostapd.conf
 hostapd hostapd.conf
 sudo airmon-ng start wlxc46e1f181d5f
 hostapd hostapd.conf
 kill -1003
 sudo kill -1003
 sudo kill -1004
 sudo kill -1148
 sudo kill -1740
 sudo kill -10011
 sudo airmon-ng start wlxc46e1f181d5f
 sudo kill -11913
 sudo kill -11925
 sudo airmon-ng start wlxc46e1f181d5f
 hostapd hostapd.conf
 sudo hostapd hostapd.conf
 ```


/etc/opt/hostapd-2.6/hostapd

test en `/etc/opt/hostapd-2.6/hostapd$ sudo st hostapd.conf `
```
interface=wlan0mon
ssid=testhotspot
wpa=2
wpa_passphrase=Chocolates35
```

```
ifconfig wlan0mon 192.168.150.1
ipaddr
nano /etc/dnsmasq.conf

bind-interfaces
interface=wlan0mon
dhcp-range=192.168.150.10192.168.150.20

etc/init.d/dnsmasq stop
etc/init.d/dnsmasq start
systemctl status dnsmasq.service


echo 1>/proc/sys/net/ipv4/ip_forward
en un nuevo bash(?)
cd -
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
iptables -A FORWARD -i wlan0mon -o eth0 -j ACCEPT
```
regresar


hostapd hostapd.conf

y en un `ap.sh`
```bash
#!/bin/bash
clear 
printf "setting IP"
sudo ifconfig wlan0mon 192.168.150.1/24
printf "enabling dhcp server"
sudo etc/init.d/dnsmasq stop
sudo etc/init.d/dnsmasq start

printf "configuring iptables"
sudo iptables -t nat -F
sudo iptables -F

sudo iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
sudo iptables -A FORWARD -i wlan0mon -o eth0 -j ACCEPT
echo 1>/proc/sys/net/ipv4/ip_forward

printf "enabling hostapd"
cd /etc/opt/hostapd-2.6/hostapd
sudo ./hostapd hostapd.conf
```

chmod 755 ap.sh
./ap.sh

sudo service NetworkManager restart


hay un error con el NetworkManager
```
gedit /etc/NetworkManager/NetworkManager.conf

y agregar

unmanaged-devices=interface-name:wlan0mon;interface-name:wlan1mon;interface-name:wlan2mon;                               # 30/08/2015: avoid conflicts with airmon-ng
```
defetos, solo corre o el wifi o el wlan0mon, creoq ue con ethernet funcionaria :'v