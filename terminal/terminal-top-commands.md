---
description: BAD
---

# Terminal top commands

## Terminal top commands

Terminal emulator on android is used for executing Linux core shells. We actually access linux commandline here

  
2. Recover wifi password and other details to which device was connected  
su  
cd data/misc/wifi  
cat wpa\_supplicant.conf

  
1. Using terminal as File Explorer without GUI  
-cd:change directory  
-pwd:shows current directory  
-ls:lists files and folders in a directory  
-cp "filename" "newfilename":copy a file

-mv "filename" "directory": move a file

-mkdir: create folder

-touch : create file

-rm:remove a file

-rmdir:remove a folder

-df:shows size of disk

-grep:capture required files from a group of files

-cat:shows file content  


| ":copy a file  |
| :--- |
| -mv "filename" "directory": move a file  |
| -mkdir: create folder  |
| -touch : create file  |
| -rm:remove a file  |
| -rmdir:remove a folder  |
| -df:shows size of disk  |
| -grep:capture required files from a group of files  |
| -cat:shows file content  |
|  |

|  |  |
| :--- | :--- |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |   -cp "filename" "newfilename":copy a file  |
|  |   -mv "filename" "directory": move a file  |
|  |   -mkdir: create folder  |
|  |   -touch : create file  |
|  |   -rm:remove a file  |
|  |   -rmdir:remove a folder  |
|  |   -df:shows size of disk  |
|  |   -grep:capture required files from a group of files  |
|  |   -cat:shows file content  |
|  |  |
|  | 3.Find internet connectivity details  |
|  |   -ping :shows data used on a particular site  |
|  |  |
|  | 4.Find hardware details.  |
|  |   -ps:shows background processors running on device  |
|  |   -date:shows date and time  |
|  |   -uptime:shows last reboot  |
|  |   -uname -a:shows os build details  |
|  |  |
|  | 5.Control network and power setting  |
|  |   -svc help:shows details about subcommands  |
|  |   -svc power:control power manager  |
|  |   -svc data:control mobile data connectivity  |
|  |   -svc wifi:control the wifi manager  |
|  |   -svc usb:control usb state  |
|  |   -svc nfc:control nfc function  |
|  |  |
|  | 6.Stop all background processes  |
|  |   dumpsys  |
|  |  |
|  | 7.Show full info of device  |
|  |   getprop  |
|  |  |
|  | 8.Reverse text order on emulator  |
|  |   rev  |
|  |  |
|  | 9.List all installed packages  |
|  |   pm list packages  |
|  |  |
|  | 10.Use terminal as app manager  |
|  |   -pm list packages \| grep "appname" :check whether app is installed or not  |
|  |   -pm disable "package name" : disable an app  |
|  |   -pm enable "package name" : enable an app  |
|  |  |
|  | 11.Shut Down device after a specified time.  |
|  |   -sleep "no. of seconds"  |
|  |  |

