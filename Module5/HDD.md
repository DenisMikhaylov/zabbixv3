```
discovery_rule
                    name: Storage file systems
                    key: Storage.discovery.config[/Storage.fs]
```
                    
```
UserParameter=custom.vfs.dev.read.ops[*],cat /sys/class/block/$1/stat | awk '{print $$1}'
UserParameter=custom.vfs.dev.read.merged[*],cat /sys/class/block/$1/stat | awk '{print $$2}'
UserParameter=custom.vfs.dev.read.sectors[*],cat /sys/class/block/$1/stat | awk '{print $$3}'
UserParameter=custom.vfs.dev.read.ms[*],cat /sys/class/block/$1/stat | awk '{print $$4}'
UserParameter=custom.vfs.dev.write.ops[*],cat /sys/class/block/$1/stat | awk '{print $$5}'
UserParameter=custom.vfs.dev.write.merged[*],cat /sys/class/block/$1/stat | awk '{print $$6}'
UserParameter=custom.vfs.dev.write.sectors[*],cat /sys/class/block/$1/stat | awk '{print $$7}'
UserParameter=custom.vfs.dev.write.ms[*],cat /sys/class/block/$1/stat | awk '{print $$8}'
UserParameter=custom.vfs.dev.io.active[*],cat /sys/class/block/$1/stat | awk '{print $$9}'
UserParameter=custom.vfs.dev.io.ms[*],cat /sys/class/block/$1/stat | awk '{print $$10}'
UserParameter=custom.vfs.dev.weight.io.ms[*],cat /sys/class/block/$1/stat | awk '{print $$11}'

UserParameter=Storage.discovery.macro[*],echo $0 | awk 'BEGIN { RS=","; FS=" "; print "{ \"data\":\n ["} {if (NR != 1 ) print(","); printf "  { \"{#FSNAME}\":\""$$1"\", \"{#FSPATH}\":\""$$2"\" }"} END{print "\n ]\n}"}'
UserParameter=Storage.discovery.config[*],cat $1 | awk 'BEGIN { FS=" "; print "{ \"data\":\n ["} {if (NR != 1 ) print(","); printf "  { \"{#FSNAME}\":\""$$1"\", \"{#FSPATH}\":\""$$2"\" }"} END{print "\n ]\n}"}'
```
