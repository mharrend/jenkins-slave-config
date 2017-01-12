# Resize the / partition
*Note*: This procedure works for Scientific Linux CERN 6 only.

The following steps will resize the / partition so it occupies the remaining space. This procedure has only been tested on the standard cloud flavors (m2.*) so care should be taken on other flavors.

```
# growpart /dev/vda 2
CHANGED: partition=2 start=821248 old: size=20150272 end=20971520 new: size=83064512,end=83885760
```

*Note*: the error message "NOCHANGE: partition 2 is size XXXXXX. it cannot be grown" can be ignored if you already resized your instance before.

The VM should then be rebooted. Once rebooted,

```
# pvresize /dev/vda2
# lvextend -l +100%FREE /dev/mapper/VolGroup00-LogVol00
# resize2fs /dev/mapper/VolGroup00-LogVol00
```
