Overview
========

How to add disks to Linux: 

1. To list the LUN ID and sd devices 
```
ls -ld /sys/block/sd*/device
```

2. Before you start identify all sd devices with this command:
```
ls /dev/sd*
smartctl --scan
``` 
 
3. Determine which host ports are in use:
```
# grep mpt /sys/class/scsi_host/host?/proc_name
/sys/class/scsi_host/host2/proc_name:mptspi 
/sys/class/scsi_host/host3/proc_name:mptspi 
```

4. Now rescan those ports (in this example host2 and host3): 
```
echo "- - -" > /sys/class/scsi_host/host2/scan 
echo "- - -" > /sys/class/scsi_host/host3/scan 
```

5. Now look for a new device with this command:
```
smartctl --scan
```
 
6. smartctl -a /dev/sde 

```
ls /sys/class/scsi_host/host?/proc_name 
for i in `ls ‐1 /sys/class/scsi_host`; do 
echo "‐ ‐ ‐" > /sys/class/scsi_host/${i}/scan 
done 

echo '1' > /sys/class/scsi_disk/0\:0\:0\:0/device/rescan 
```