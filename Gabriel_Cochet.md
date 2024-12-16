# b1linux2

Gabriel Cochet 

### installer nginx

```
root@debian:~# apt install nginx
```

### sécuriser nginx et le serveur 

```
root@debian:~#  firewall-cmd --list-all
public
  target: default
  icmp-block-inversion: no
  interfaces:
  sources:
  services: dhcpv6-client ssh
  ports:
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

```
root@debian:~# firewall-cmd --set-log-denied=all
success
```

```
root@debian:~# firewall-cmd --zone=public --add-service=http --permanent
firewall-cmd --zone=public --add-service=https --permanent
success
success
```

```
root@debian:~# firewall-cmd --set-default-zone=drop
success
```


```
root@debian:~#  firewall-cmd --reload
success
root@debian:~#  firewall-cmd --list-all
public
  target: default
  icmp-block-inversion: no
  interfaces:
  sources:
  services: dhcpv6-client http https ssh
  ports:
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

```
root@debian:~# chmod 644 /etc/nginx/sites-enabled/*
root@debian:~# chmod 644 /etc/nginx/sites-available/*
root@debian:~# chmod 644 /etc/nginx/nginx.conf
```


```
root@debian:~# useradd Gabi
root@debian:~# passwd Gabi
New password:
Retype new password:
passwd: password updated successfully
mdp root : Gabito29
```

```
root@debian:~# firewall-cmd --list-all
drop
  target: DROP
  icmp-block-inversion: no
  interfaces:
  sources:
  services: http https ssh
  ports:
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

```
sudo apt install  fail2ban
```

```
sudo nano /etc/fail2ban/jail.local
```

```
[sshd]
enabled = true
port = ssh
logpath = /var/log/secure
maxretry = 5
```


```
root@debian:~# sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

```
root@debian:~# sudo fail2ban-client status sshd
Status for the jail: sshd
|- Filter
|  |- Currently failed: 0
|  |- Total failed:     0
|  `- File list:
`- Actions
   |- Currently banned: 0
   |- Total banned:     0
   `- Banned IP list:
```