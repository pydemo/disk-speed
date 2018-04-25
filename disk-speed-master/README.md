# disk-speed
Measure disk speed from Python by writing to disk. 
The disk can be SSD, HDD, eMMC, flash drive, NAS, Cloud, as long as it is mounted and writable.

The measurement will take 0.5 second.

# Purpose

Loosely measure the speed of a 'disk', in order to note the speed difference between a SSD and a Cloud mount.

# Usage:

Without parameter:

```
$ ./diskspeed.py 
Absolute path of filename  /home/sander/disk-speed/outputTESTING.txt
Disk writing speed: 154.509901638 Mbytes per second
```



With a parameter specifying the directory to be tested:
```
$ ./diskspeed.py /home/sander/
Absolute path of filename  /home/sander/outputTESTING.txt
Disk writing speed: 143.504647188 Mbytes per second
```

With a different directory specified, in this case a mount on a remote server
```
$ ./diskspeed.py '/run/user/1000/gvfs/sftp:host=server.example.com,port=2222/home/sander/'
Absolute path of filename  /run/user/1000/gvfs/sftp:host=server.example.com,port=2222/home/sander/outputTESTING.txt
Disk writing speed: 0.569606459526 Mbytes per second
```
Speed of a NAS on my LAN mounted via SMB:
```
$ python diskspeed.py '/run/user/1000/gvfs/smb-share:server=192.168.1.165,share=share'
Let's go
Disk writing speed: 0.69 Mbytes per second
Done

```

# Usage Module

```
import diskspeed
print diskspeed.diskspeedmeasure('/tmp')
print diskspeed.diskspeedmeasure('/tmp/')
```
or
```
from some.path.diskspeed import diskspeedmeasure
print diskspeedmeasure('/tmp')
```

# Accuracy

Speed measured this speed is not too far away from the Real Stuff with hdparm:
```
$ sudo hdparm -tT /dev/sda6 | tail -1
 Timing buffered disk reads: 618 MB in  3.00 seconds = 205.86 MB/sec
```

# Results

Disk type  | Result in Mbytes/s
------------- | -------------
SSD  | 132.7
eMMC | 62.4
Flash card  | 18.1
Flash card (Raspi) | 3.6
Lacie NAS on wired LAN | 3.2
Some NAS on LAN | 2.2
SFTP mount over Internet | 0.57
Lacie NAS via WLAN | 0.21


 


