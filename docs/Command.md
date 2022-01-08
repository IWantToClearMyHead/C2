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
| mount | mount -o loop src.iso /dst | |
| umount | umount /dst | |
| comp tar | tar -cvf xxx.tar xxx | |
| decomp tar | tar -xvf xxx.tar | |
| comp tar.gz |  | |
| decomp tar.gz | tar -zxvf xxx.tar | |
| comp xz | tar -cvf xxx.tar xxx<br>xz -z xxx.tar | |
|decomp xz | tar -Jvf xxx.tar.xz | |
| comp bz2 |  | |
|decomp bz2 | tar -jvf xxx.tar.xz | |

### Git
| type | command | note |
| -----| ---- | ---- |
| show |  git config --list --show-origin | |
| delete after commit | git restore --source=HEAD^ --staged  -- path/*.* | |

### Screen
| type | command | note |
| -----| ---- | ---- |
|detach |  Ctrl + A, d | |
|retach |  screen -r pid | |
|list |  screen -ls | |

<a href="#top">Back to top</a>
