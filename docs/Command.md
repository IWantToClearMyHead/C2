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
|download a file|curl -O http://baidu.com/uploads/a.bb||
| awk last column | awk '{print $0}' a.txt | [awk](Command_AWK.md) |
| grep number |ls benchspec/CPU/ \| grep -E '[0-9]{3}' \| wc -l||
| echo flash |echo -e "\033[44;37;5m flash \033[44;37;0m"||
| cd in script |. ./a.sh||
| clear content| : > a.txt ||
|delete many ps|ps aux | grep FVP | awk '{print $2}' | xargs kill -9|
|show column 2 and 3|cut -d' ' -f2,3|
|make folder into html|tree -C -L 3 -T "fvpdoc" -H "index.html" -I "node_modules" --charset=gbk -o ooTree.html|
|make html|ansifilter -i css.cfg1 -H -o css.cfg1.html|
|delete a file start with dash|rm -- -H|
|newest file in folder|find . -type f -printf "%T@ %p\n" \| sort -n \| cut -d' ' -f 2- \| tail -n 1|
|align via awk|sudo cat /proc/1/maps \| awk '{printf("%-35s %-s\n", $1, $6);}'|
|show files in better format|ls -l \| awk '{printf("%6s %s %2s %s %-s\n", $5, $6, $7, $8, $9);}'|

<!---
div class="special-class" markdown="1"
is not working...


-->


### SVN
| type | command | note |
| -----| ---- | ---- |
||svn co https://svn.internal.foo.com/svn/mycoolgame/branches/1.81||
|create your new file|||
||svn add your new file||
||svn ci -m "added file lalalalala" you new file||

### Git
| type | command | note |
| -----| ---- | ---- |
| show |  git config --list --show-origin | |
| delete after commit | git restore --source=HEAD^ --staged  -- path/*.* | :heavy_multiplication_x: |
| check tag |git clone -b vx.x.x.x https://gem5.googlesource.com/public/gem5||
| clean build |git fetch origin<br>git checkout branchname<br>git reset --hard origin/branchname<br>git  clean -d --force||



### Screen
| type | command | note |
| -----| ---- | ---- |
|detach |  Ctrl + a, d | |
|rettach |  screen -r pid | for dettached |
| |  screen -rd pid | for attached |
|list |  screen -ls | |
|kill a detached|screen -S 1186535 -X quit||
|con tcp|screen //telnet 127.0.0.1 5018||
|switch|Ctrl + a, Ctrl + a||
|lock|Ctrl + a, x|need input password|
|kill current|Ctrl + a, k, y|no to cancel|


### Misc
| type | command | note |
| -----| ---- | ---- |
| make to show variable |  $(warning  $(XXX)) | |
| make log | make 2>&1 | tee log | |
| gcc log | gcc a.c > log 2>&1 | |


<a href="#top">Back to top</a>
