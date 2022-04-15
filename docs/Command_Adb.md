### server-side

```
#ssh 920 use robox
cd ~/robox_920_huawei/script/download/robox/binaryFiles
./robox start 1
netstat -tlp | grep 5559
adb connect 192.168.10.111:5559
scrcpy -s 192.168.10.111:5559
http://192.168.10.111:8090/files
adb install zd.apk
#success
#inside anbox
adb shell
#inside 920
perf

```

<a href="#top">Back to top</a>
