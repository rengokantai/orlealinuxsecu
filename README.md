#### orlealinuxsecu
#####Firewalls
######iptables
```
 sysctl -w net.ipv4.ip_forward=1
 ```
 to change this permanently
 ```
 vim /etc/sysctl.conf
 ```
 vim
 ```
 vim fw.rules
 ```

edit
```
/sbin/iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
/sbin/iptables -A FORWARD -i eth0 -o eth1 -m state --state RELATED,ESTABLISHED -j ACCEPT
/sbin/iptables -A FORWARD -i eth1 -o eth0 -j ACCEPT
```
######iptables tables
```
iptables -t mangle --list
```
######matching on protocol
```
iptables (-t filter) -A INPUT -p tcp --tcp-flags SYN,FIN,PSH,URG
```
######rate limiting
-m match
```
iptables -A INPUT -p tcp --syn -m limit --limit 1/s -j ACCEPT
```
######new versus established versus related
```
iptables -A INPUT -m state --state NEW -j ACCEPT
```
######iptables with multiple interfaces
```
iptables -A INPUT -i eth0
iptables -A FORWARD -i eth0(local) -o eth1 (internet) -p tcp --sport(source port) -j ACCEPT
```
######firewalld
check state
```
firewall-cmd --state
```
```
firewall-cmd --get-zones
```

######ufw
usage
```
ufw enable/disable
ufw status verbose
ufw allow 80/tcp
ufw delete deny 8080/tcp
ufw deny 8080/tcp
ufw allow ssh
```
just check
```
less /etc/services
```
######gufw
