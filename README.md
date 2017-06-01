# OpenVZ 7 / Virtuozzo 7 Goodies


### Initial [Devuan](https://devuan.org/) 1.0 template support.
Based on a mix of the Debian 7 and 8 templates.

Only the 'minimal' install has been tested.

1. Place the devuan directory in /vz/templates
2. Add the following to: /vz/template/conf/vztt/url.map
```

$DEVUAN_SERVER  http://auto.mirror.devuan.org

```

3. Setup network:
```
prlctl set Devuan --ipadd 192.168.5.101/24
prlctl set Devuan --nameserver 8.8.8.8

```

Make sure your server is configured as per: https://openvz.org/Using_NAT_for_container_with_private_IPs

4. Then run:
```
vzpkg create cache devuan-1.0-x86_64-minimal
prlctl create MyDevuan --vmtype ct --ostemplate devuan-1.0-x86_64-minimal
prlctl start MyDevuan
prlctl enter MyDevuan
```
4. PROFIT!


#### TODO:
Sysvinit cleanup of 'sysvinit: restarting...init: timeout opening/writing control channel /run/initctl'

#### Known Issues:

1. devuan-baseconf not properly activating, so taken over by post-install
2. mknod messages should be supressed
3. initctl shouldn't try to run or shouldn't/should fail cleanly.
