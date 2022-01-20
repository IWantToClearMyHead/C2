### Windows

| type | command | note |
| -----| ---- | ---- |
| cmd in english | chcp 43 |  
| cpu detail | wmic cpu get /format:hform > cpu.html | 
| memory detail | wmic memorychip |  
| hard disk | wmic diskdrive list full /format:hform > hdd.html |

### Linux

| type | command | note |
| -----| ---- | ---- |
| hard disk | diskpart | |
| folder sort |  du -s * \| sort -rn | |
| current path folder size|du -h --max-depth=1 .||
| total folder size |du -h --max-depth=1 folder||
| mount | mount -o loop src.iso /dst | |
| umount | umount /dst | |
| comp tar | tar -cvf xxx.tar xxx | |
| decomp tar | tar -xvf xxx.tar | |
| comp tar.gz | tar -czf xxx.tar xxx | |
| decomp tar.gz | tar -xzf xxx.tar | |
| comp xz | tar -cvf xxx.tar xxx<br>xz -z xxx.tar | |
|decomp xz | tar -Jvf xxx.tar.xz | |
| comp bz2 | tar -cjf xxx.tar.bz2 xxx | |
|decomp bz2 | tar -jvf xxx.tar.xz | |
| kill all commands |ps aux | grep runcpu |  awk {'print $2}' | sudo xargs kill -9| root no need sudo|
| ls in one line | ls \| xargs| |
| ls in one column | ls -1 | |
| nc passfile | | |
| receiver | nc -l -p #port > passfile | |
| sender | nc -w 3 [receiver #ip] #port < passfile | |
|download a file|curl -O http://192.168.10.164:8000/uploads/a.bb||


### Git
| type | command | note |
| -----| ---- | ---- |
| show |  git config --list --show-origin | |
| delete after commit | git restore --source=HEAD^ --staged  -- path/*.* | :heavy_multiplication_x: |
| check tag |git clone -b vx.x.x.x https://gem5.googlesource.com/public/gem5||
||||

### Screen
| type | command | note |
| -----| ---- | ---- |
|detach |  Ctrl + A, d | |
|rettach |  screen -r pid | for dettached |
| |  screen -rd pid | for attached |
|list |  screen -ls | |
|kill a detached|screen -S 1186535 -X quit||

### Misc
| type | command | note |
| -----| ---- | ---- |
| make to show variable |  $(warning  $(XXX)) | |
| make log | make 2>&1 | tee log | |
| gcc log | gcc a.c > log 2>&1 | |


<a href="#top">Back to top</a>
