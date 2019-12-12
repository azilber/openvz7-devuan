penVZ 7 / Virtuozzo 7 Goodies


### [Devuan](https://devuan.org/) 1.0 & 2.1 template support.
Based on a mix of the Debian 7-10 templates and Devuan vbox.

Only the 'minimal' install has been tested for Devuan 1.0.
Devuan Ascii (2.0) only has the regular install (which is basically minimal).

Devuan 1.0 should be considered deprecated.

### Instructions:

1. Place the devuan directory in /vz/templates
2. Add the following to: /vz/template/conf/vztt/url.map

```
For Devuan Jessie and ASCII:
$DEVUAN_JESSIE  http://auto.mirror.devuan.org
$DEVUAN_ASCII  http://deb.devuan.org
```
  
3. List OS Templates:
```
vzpkg list -O --with-summary |grep -i devuan

devuan-2.0-x86_64                  :Devuan Ascii 2.1 (for AMD64/Intel EM64T) Virtuozzo Template
devuan-1.0-x86_64                  :Devuan 1.0 (for AMD64/Intel EM64T) Virtuozzo Template
devuan-1.0-x86_64-minimal          :Devuan 1.0 minimal (for AMD64/Intel EM64T) Virtuozzo Template
```

4. Setup Cache and Container:
```
vzpkg create cache devuan-1.0-x86_64-minimal
vzpkg create cache devuan-2.0-x86_64
prlctl create Devuan --vmtype ct --ostemplate devuan-1.0-x86_64-minimal
prlctl create Devuan2 --vmtype ct --ostemplate devuan-2.0-x86_64
```

5. Setup network (optional):
```
prlctl set Devuan --ipadd 192.168.5.101/24
prlctl set Devuan --nameserver 8.8.8.8
```

Make sure your server is configured as per: https://openvz.org/Using_NAT_for_container_with_private_IPs

6. Then run:
```
prlctl start Devuan
prlctl enter Devuan
```

7. PROFIT!


#### Known Issues:

1. devuan-baseconf not properly activating, so taken over by post-install
2. mknod messages should be supressed
3. initctl shouldn't try to run or shouldn't/should fail cleanly.

