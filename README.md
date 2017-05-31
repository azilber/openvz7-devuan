# OpenVZ 7 / Virtuozzo 7 Goodies


### Initial [Devuan](https://devuan.org/) 1.0 template support.
Based on a mix of the Debian 7 and 8 templates.

Only the 'minimal' install has been tested.

1. Place the devuan directory in /vz/templates
2. Add the following to: /vz/template/conf/vztt/url.map
```

$DEVUAN_SERVER  http://auto.mirror.devuan.org

```
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

Network testing
